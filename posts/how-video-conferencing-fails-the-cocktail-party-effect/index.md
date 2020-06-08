<!--
.. title: How video conferencing fails the cocktail party effect
.. slug: how-video-conferencing-fails-the-cocktail-party-effect
.. date: 2020-04-28 17:06:58 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

I've been attending a lot of video conferences lately. Some of them meet the definition of a *meeting*: 3-20 people in a room, with one person speaking while everyone else listens. This is a well-understood UX paradigm, decently served by the likes of Zoom, Google Hangouts and Jitsi and originated in the business world as a natural corollary to conference calls over the telephone.

## Zoom parties are pathetic

A lot of my recent video calls do not **at all** fit into the *video-conferencing* paradigm: They are virtual social gatherings, intended to fulfill the need for community, human connection and fun in times of social distancing. Most of them should not meet the basic criterion of a meeting: There's no agenda. Usually there's more than one topic and more than one person wanting to speak at any given time. These get-togethers are shoe-horned into a User Experience that has very little to do with their intended reality: a loose, multi-stranded interaction.  In normal social gatherings, even if it's just four or five people, there is a natural ebb-and-flow from joint conversation to breaking off to talk about something in private, or even overhearing a word and joining back in (the famed [cocktail party effect](https://en.wikipedia.org/wiki/Cocktail_party_effect)).

The *cocktail party effect* is related to a basic human need: Ambient social awareness, which makes social gatherings interesting, fulfilling and comforting. We want to know who is talking to whom. **But**, we don't want to be *forced to listen* to every word they say. In video calls it's so easy to get impatient, waiting for a turn to get a word in edgewise. While I love my friends, they can be tedious at times. This is exacerbated by the fact that most video conferencing apps practice active noise-suppression: They are specifically targeted at letting only one source speak at any given time. 

There have been some [great](https://tedcooke.blog/2020/04/13/21-things-we-learned-from-hosting-our-first-online-party/) [attempts](https://www.houseparty.com/) at enabling multiple parallel conversations, using *breakout-rooms*: sub-sessions of a conference call, which can be easily reachable from the main context. However, the hard break between main and breakout room still remains.

On the internet, software shapes social interaction. This is nothing new, in the real world we shape our social interactions all the time. There are clear differences between the kinds of connections you can have in a noisy dive bar, an office break room, at home in your living room, on a factory floor, or while out together on a forest hike. As developers of social apps we should be able to formulate clearly what kind of social interaction we are looking to shape. Is it productive? Confrontational? In-depth or fleeting? Warm or impersonal?

Zoom calls shape a kind of social connection that may be effective for jointly pursuing a work-related agenda. But it falls flat when trying to, you know, *actually connect*. We also should not kid ourselves into believing that social needs are purely a matter of private life. If we are to make remote work viable at scale, we have to take them into account.

## Criteria for a good social gathering app

In short, we want:

- Multiple adjacent conversations,
- aware of each other's participants and content,
- without interfering with each other.

Additionally we may also appreciate:

- a shared context or world to inhabit, things to look at or manipulate together.
- the ability to pass by, casually join or leave a conversation: in-between-states.

The most natural realm in which these sorts of casual/world-driven dynamics have played out online are multiplayer games. For many individuals and some social groups, games have been a great way to spend time together: It's not by accident that games such as [Animal Crossing](https://www.animal-crossing.com/) have been a hit in the recent COVID-months. But even the best of games will always be attractive to some, but boring to others, even amongst people who "like games" there will be a variety of opinions about which game to choose. So if you want to have a *social* gathering, focused on the social interaction rather than on the world it's embedded in, you may want to turn elsewhere.

## Spatial social software

One compelling idea has been to embed people as avatars in a simple virtual 2D or 3D space, using text, audio and/or video communication. (See: [Spatial Software](https://darkblueheaven.com/spatialsoftware/), [Avatar chat apps](https://extendedmind.io/blog/2020/3/20/video-conferencing-wont-cure-loneliness-avatar-chat-apps-can-help), [Spontaneous social apps](https://techcrunch.com/2020/04/18/clubhouse-app-chat-rooms/)) The watch-word here is *simple*: most recent approaches have eschewed going full-bore 2nd life -- instead they  offer more abstract UX primitives, such as an abstract 2D space, in an attempt to sufficiently model some selection of the criteria for a *good social gathering app* I put forth above.

"Conversation adjacency" in these apps is organized in three rough categories:

- a list or tree of individual rooms
- two-dimensional spatial embedding
- three-dimensional embedding

## VEEPARTY

Many of these realtime-social apps look really fun and interesting, but most have *either* a spatial context (with artificial avatars)() *or* video chat. Ultimately I actually want to see *and* hear my friends in an explorable setting.
Under normal circumstances my gripes with video conferencing would have lain fallow as I wait for someone else to fix it, but as fate willed it I had some time on my hands and was stuck at home. -- So I put together a webrtc app to play around with the above requirements list: [https://veeparty.horse](https://veeparty.horse)

Veeparty is a video chat app embedded in a zoomable 2D space. 

- Users are represented by a circular video avatar that they can move around freely.
- Every user has a defined "earshot radius" in which they can hear others.
- Other participants beyond that radius can not be heard, but you can see a real-time transcription of what they are saying at a glance (hence approximating the cocktail party effect).
- Users can draw and write on the background and embed images, making the space their own and having fun.
- You can create a new space for you and your friends or join an existing public space.

[Online Town](https://theonline.town) is a closely related app. It has a simple interface, embedded in a 2D space, people are able to move around and there is a notion of distance and radius-of-hearing. I do have number of differences of opinion when it comes to User Experience, but I invite you to form your own opinion!

# Zoom meets Minecraft

In playing around with veeparty, I've had the growing sense that there's maybe an interesting new category of app here: Something that's decidedly not a game, but nevertheless integrates many playful / world building aspects. An app that you might even play games inside of but that fundamentally is just a simple world for people to meet in and interact.
In a way this hearkens back to the early era of facebook apps (and perhaps there are a number of lessons to be learned from that cautionary tale).

For now the plan is to keep adding simple primitives for fun interactions between friends or strangers. My app is still very rough around the edges and only supported on Desktop Firefox and Chrome, so [check it out](https://veeparty.horse) with that in mind.