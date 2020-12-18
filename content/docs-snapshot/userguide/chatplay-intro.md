# Twitch ChatPlay System<a name="chatplay-intro"></a>

Twitch ChatPlay provides a flexible framework to create customized game interactions between broadcasters and spectators on Twitch, the world’s leading social video platform and community for gamers\.

Twitch ChatPlay includes support for chat commands, polls, and surveys that can be triggered by Twitch viewers through the Twitch chat channel\. For example, you can create a chat command \#cheer that triggers celebration animations in your game\.

Twitch ChatPlay is implemented by a set of Script Canvas nodes that establish a connection to a Twitch channel and use incoming traffic as a game input, like any other input device\.

Twitch ChatPlay includes the following components and services:
+ Twitch IRC servers
+ Twitch ID authentication
+ Twitch account

The following diagram illustrates Twitch ChatPlay's server\-side components\.

![\[Twitch ChatPlay server-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/chatplay/chatplay-server.png)

The following diagram illustrates Twitch ChatPlay's client\-side components\.

![\[Twitch ChatPlay client-side components\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/chatplay/chatplay-client.png)

**Topics**
+ [Twitch ChatPlay Console Variables, Classes, and Connection Methods](chatplay-console-variables.md)
+ [Create a Twitch Client ID for use with Twitch ChatPlay in Lumberyard](chatplay-generate-twitch-client-id.md)