
The step builder [[Design Pattern]] is an extension on the ideas in the [[Builder]] pattern. In this pattern the construction of objects is broken down into steps.

Doing it this way has some advantages
- It guides the consumer of the code through the creation process
- It prevents the consumer to call `build()` in invalid states
- it Prevents large amounts of required parameters in the build method or constructor
- It can support branching options

It however does come with some drawbacks in comparison to the traditional builder. Mainly it can be overcomplicated for simple use casess, as well as the fact its hard to retroactiviely change previous steps values (if your using one builder to make multiple objects this would cause issues). Also if you make the step builder in the way of the example below, a consumer can also break the code via casting.

# Example

In the below example you can see the step builder in action. 

In this example we are creating a subway sub.

In a subway sub Bread and Fillings are required, to make this enforced by the builder we make there no way to get to the next step apart from passing the Bread and Filling data. 

Although we can probably assume that a subway sub is toasted by default, it may not be clear to a consumer of the code what the default is, here you see we force the consumer to tell us toasted or not toasted.

Toppings are optional, and therefore the topping step has the functions and methods of the next state, the build step. 

You can also have multiple toppings, so we return the same step when we add a topping. 

When we add a topping, we also branch out into the more toppings step, which allows for the last topping to be added again. This is an example of how it can be used for branching

```kt
import kotlin.system.*

enum class BreadType {
    ITALIAN_WHITE,
    HEARTY_ITALIAN,
    NINE_GRAIN,
    HERBS_CHEESE,
    TIGER_BREAD,
    WRAP,
    GLUTEN_FREE
}

enum class Filling {
    MEAT_BALLS,
    CHICKEN_TIKA,
    HAM,
    SPICY_ITALIAN,
    VEGGIE
}

enum class Topping {
    JALAPENO,
    PICKLE,
    PEPPER,
    LETTUCE, 
    CUCUMBER
}

class Sub(val bread : BreadType,
    val filling : Filling, 
    val isHot : Boolean,
    val toppings : List<Topping>   
){	
    override fun toString() : String {
		return "bread : $bread\nfilling : $filling\nisHot : $isHot\ntoppings : { ${toppings.joinToString()} }"
    }
    
    companion object {
        fun builder() : BreadStep { return Builder() }
    }
    
    interface BreadStep {
    	fun withBread(bread : BreadType) : FillingStep
    }
    
    interface FillingStep {
    	fun withFilling(filling : Filling) : HeatStep
    }
    
    interface HeatStep {
    	fun toasted() : ToppingsStep
        fun notToasted() : ToppingsStep
    }
    
    interface ToppingsStep : BuildStep {
    	fun withTopping(topping : Topping) : MoreToppingsStep
    }
    
    interface MoreToppingsStep : ToppingsStep {
    	fun morePlease() : MoreToppingsStep
    }
    
    interface BuildStep {
    	fun build() : Sub
    }
	
    private class Builder : BreadStep, FillingStep, HeatStep, ToppingsStep, MoreToppingsStep, BuildStep {
        private lateinit var _bread : BreadType
        private lateinit var _filling : Filling
        private var _isHot : Boolean = false
		private var _toppings : MutableList<Topping> = mutableListOf()
        private lateinit var lastTopping : Topping 
        
        override fun withBread(bread : BreadType) : FillingStep {
            _bread = bread
            return this
        }
        
        override fun withFilling(filling : Filling) : HeatStep {
            _filling = filling
            return this
        }
        
        override fun toasted() : ToppingsStep {
            _isHot = true
            return this
        }
        
        override fun notToasted() : ToppingsStep {
            _isHot = false
            return this
        }
        
        override fun withTopping(topping : Topping) : MoreToppingsStep {
            _toppings.add(topping)
            lastTopping = topping
            return this
        }
        
        override fun morePlease() : MoreToppingsStep {
            _toppings.add(lastTopping)
            return this
        }
        
        override fun build() : Sub {
            return Sub(_bread, _filling, _isHot, _toppings)
        }
    }
}

fun main(){
   var simpleSub = Sub.builder()
   		.withBread(BreadType.GLUTEN_FREE)
   		.withFilling(Filling.VEGGIE)
   		.notToasted()
   		.build()
        
    println("-- simple sub --\n${simpleSub}")
    
   var complexSub = Sub.builder()
   		.withBread(BreadType.HEARTY_ITALIAN)
   		.withFilling(Filling.SPICY_ITALIAN)
   		.toasted()
   		.withTopping(Topping.PEPPER)
   		.morePlease()
   		.withTopping(Topping.JALAPENO)
   		.build()
   println("\n-- complex sub --\n${complexSub}")
}
```