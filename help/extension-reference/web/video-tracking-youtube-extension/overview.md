---
title: Video Tracking | YouTube Release Notes
seo-title: Video Tracking | YouTube Release Notes for Adobe Experience Platform Launch
description: Video Tracking | YouTube Release Notes for Adobe Experience Platform Launch
seo-description: Video Tracking | BrightCove Release Notes for Adobe Experience Platform Launch
---

# Video Custom Cue Tracker: YouTube extension documentation

**Prerequisites**

Each Adobe Experience Platform Launch property requires that the following extensions are installed and configured from the Extensions screen:

* Adobe Analytics
* Experience Cloud Visitor ID Service
* Core extension

Per [https://developers.google.com/youtube/player_parameters](https://developers.google.com/youtube/player_parameters), use the ”Embed a player using an tag” code snippet in the HTML of each Web page where a video player is to render.

This extension version 1.0.0 supports embedding one or more YouTube videos on a single Web page by inserting an `id` attribute with a unique value in the iframe tag, and appending `?enablejsapi=1` to the end of the `src` attribute value. For example:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Because the extension dynamically adds the `id` field and `enablejsapi=1` query string parameter to the iFrame dynamically, do not add these to the iFrame manually.

On pages with more than one video, note that each video uses the same configuration set in the Platform Launch rule executing on that page. For example, if you create a rule with an event that triggers on video 50% complete, each video on the page triggers the rule at the 50% cue point.

The extension relies on the following logic to rewrite the iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Therefore, there will be a slight flicker after the page loads. This behavior is expected.

## Data elements

There are five data elements available within the extension, none of which require configuration.

* **Playhead Position:** Records the place, in seconds, of the playhead position on the video timeline, when it is called upon within a Launch Rule.
* **Video ID:** Specifies the YouTube ID associated with the video.
* **Video Name:** Specifies the descriptive, or friendly name of the video.
* **Video URL:** Returns the YouTube.com URL for the currently loaded/playing video.
* **Video Duration:** Records the total duration, in seconds, of the video content.

## Events

There are seven events available within the extension, only Custom Cue Point Tracking requires configuration.

* **Video Ready:** Triggers when the video is cued, and ready to play.
* **Video Start:** Triggers when the video is first started, and when `player.getCurrentTime() === 0`
* **Video Pause:** Triggers when the video is paused.
* **Video Resume:** Triggers when the video is resumed, and when `player.getCurrentTime() !== 0`
* **Custom Cue Tracking:** Triggers when the video reaches the specified video threshold percentage. 
  For example, if a video is 60 seconds and the specified cue point is 50%, the event with trigger when the playhead position equals 30 seconds. Cue point tracking applies to both initial play and replay. Note that if user seeks across a cue point, the event will not fire. Cue point events only fire when the playhead crosses the calculated cuepoint location on the timeline, and video player is playing.
* **Video Buffer:** Triggers when the player downloads a certain amount of data before it begins playing the video.
* **Video Ended:** Triggers when a video fully completes.

## Usage

There os one Platform Launch rule for every video event (listed above). You need to create a specific rule for each event you want to track. In other words, if you don't want to track Video Pause, you wouldn't create a rule for it.

Rules have three actions:

* **Set variables:** Set the Adobe Analytics variables (map to all or some included data elements).
* **Send beacon:** Send the Adobe Analytics beacon as a custom link tracking call, and provide a ”Link Name” value.
* **Clear variables:** Clear the Adobe Analytics variables.

**Example Platform Launch rule for ”Video Start”**

The following Video Extension objects are to be included.

Events:

”Video Start” (This event causes the rule to fire when the visitor starts playing a YouTube video.)

Condition: None

Actions: Use the Analytics extension to:

1. ”Set Variables” action, to map:
  * The event for Video Star,
  * A prop/eVar for the Video Duration data element
  * A prop/eVar for the Video ID data element
  * A prop/eVar for the Video Name data element
  * A prop/eVar for the Video URL data element
1. Then, include the ”Send Beacon” action (`s.tl`) with link name ”video start," followeded by a ”Clear Variables” action.

>[!Tip]
> 
> For implementations where multiple eVars or props for each video element can't be used, data element values can be concatenated within Platform Launch, parsed into classification reports using the Classification Rule Builder tool, as explained in [https://docs.adobe.com/content/help/en/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://docs.adobe.com/content/help/en/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html), and then applied as a segment in Analysis Workspace.

To concatenate video information values, create a new data element called ”Video Meta Data,” and program it to pull in all the video data elements (listed above) and assemble them together. For example:

```javascript
var r = ””;

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));

return r.join('|');
```
