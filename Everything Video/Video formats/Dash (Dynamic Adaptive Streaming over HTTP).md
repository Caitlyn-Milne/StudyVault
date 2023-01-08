Dash (aka Dynamic Adaptive Streaming over Http) is an adaptive video streaming technique that as the name suggests uses http to deliever media content.

Dash allows for different media tracks to be swapped between, such as to vary the bitrate / quality of the video, or change the audio track as in the case for language features.

Choosing between multiple tracks of different bitrates can allow for choosing a higher bandwidth but higher quality video when the internet is good, but when the internet quality is poor, a lower quality track can be chosen.

Since alot of players such as [[Exoplayer]] load only a segment of video data at a time, this means you can start watching a video with great internet, with the high bitrate track being selected, but as internet gets worse, the lower bitrate track can be used to fill the buffer up, then when the internet gets better, the buffer can then again be filled with higher bitrate data.

## mpd
`.mpd` files (media presentation description) are used for dash to describe the previously mentioned information, this includes what codecs are being used, urls to each track, and so on. 

Heres an example of an example mdp file taken from a google example project
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--Generated with https://github.com/google/shaka-packager version 97fc982-release-->
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xlink="http://www.w3.org/1999/xlink" xsi:schemaLocation="urn:mpeg:dash:schema:mpd:2011 DASH-MPD.xsd" xmlns:cenc="urn:mpeg:cenc:2013" minBufferTime="PT2S" type="static" profiles="urn:mpeg:dash:profile:isoff-on-demand:2011" mediaPresentationDuration="PT734S">
  <Period id="0">
    <AdaptationSet id="0" contentType="audio" lang="en">
      <Representation id="0" bandwidth="131596" codecs="mp4a.40.2" mimeType="audio/mp4" audioSamplingRate="44100">
        <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
        <BaseURL>tears_audio_eng.mp4</BaseURL>
        <SegmentBase indexRange="745-1664" timescale="44100">
          <Initialization range="0-744"/>
        </SegmentBase>
      </Representation>
    </AdaptationSet>
    <AdaptationSet id="1" contentType="video" maxWidth="1920" maxHeight="856" frameRate="12288/512" par="38:17">
      <Representation id="1" bandwidth="769255" codecs="avc1.42c01e" mimeType="video/mp4" sar="852:857" width="320" height="142">
        <BaseURL>tears_h264_baseline_240p_800.mp4</BaseURL>
        <SegmentBase indexRange="827-1602" timescale="12288">
          <Initialization range="0-826"/>
        </SegmentBase>
      </Representation>
      <Representation id="2" bandwidth="1774254" codecs="avc1.4d401f" mimeType="video/mp4" sar="2242:2249" width="854" height="380">
        <BaseURL>tears_h264_main_480p_2000.mp4</BaseURL>
        <SegmentBase indexRange="829-1604" timescale="12288">
          <Initialization range="0-828"/>
        </SegmentBase>
      </Representation>
      <Representation id="3" bandwidth="7203938" codecs="avc1.4d4028" mimeType="video/mp4" sar="855:857" width="1280" height="570">
        <BaseURL>tears_h264_main_720p_8000.mp4</BaseURL>
        <SegmentBase indexRange="830-1605" timescale="12288">
          <Initialization range="0-829"/>
        </SegmentBase>
      </Representation>
      <Representation id="4" bandwidth="18316946" codecs="avc1.64002a" mimeType="video/mp4" sar="856:857" width="1920" height="856">
        <BaseURL>tears_h264_high_1080p_20000.mp4</BaseURL>
        <SegmentBase indexRange="832-1607" timescale="12288">
          <Initialization range="0-831"/>
        </SegmentBase>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```