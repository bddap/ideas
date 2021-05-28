# Intro

Media streaming services including both video streaming and audio streaming services provide two primary features, content licensing and data provision.

A video streaming service, for example, will, *license* content from the copyright holder, and *provide* the content to customers by streaming it over the network.

# Idea

Separate licensing from data provision. Allow copyright holders to issue licenses to consumers directly or indirectly. When a consumer proves they have a license to some media, a data provider may send that data to the user (i.e. via streaming or by sending the media in full).

Data providers may be paid services, or they may even be built upon p2p networks such as ipfs or bittorrent.

You might think of the idea as a licensing layer that allows the distribution and consumption of copyrighted material in a legal and ethical way, a way that skips intermediaries, allowing copyright holders to license directly to consumers without needing to build their own streaming service.

# Motivations

## Music Library Data

I don't like the data describing my music library (likes, play-counts, playlists) to be locked into a specific service. I use streaming service X for it's recommendation engine, but I would much prefer to own my music library data, using a separate standalone service or program for recommendation.

My ideal vision has me licensing music from service A, B and C and also directly from artists. My music library data and recommendations would be handled separately from licensing and data provision. I would handle my own p2p node.

This setup can also apply to other media types not just music. The same system can handle music, video, software, and other types of media all via the same protocols.

## Remove Intermediaries; Market Efficiency

Streaming services take a substantial cut of streaming revenue, granting only a fraction of that revenue to copyright holders. If copyright holders could issue licenses directly to consumers, 100% of revenue could go directly to copyright holders.

## Explosion Of Video Streaming Services

I am subscribed to HBO max, Netflix, Amazon Prime, Disney+, Hull and more. I need to use different software depending on what I want to watch. I would rather let each of these platforms be a licensing provider and use a single software of my choice to stream anything for which I have a license.

A benefit to this approach is that I control a copy of my personal library data (watch list, view counts). I won't lose that data when canceling a service. I get to choose which recommendation engine, if any, that I want to use.

## Metadata Silos

Each streaming service keeps its own media metadata. A free, open, and interoperable global metadata store allows for deduplication of effort and for new use-cases.

## P2P Content Distribution Without Piracy

Current p2p content distribution technology is capable and convenient for distribution. Segregated licensing introduces a convenient way to use these networks while respecting copyright.

## Rhythm Games

Rhythm games provide two forms of content simultaneously, a music track and a choreography track. The musician is likely to be a separate entity from the choreographer. The rhythm game is effectively a media player that plays both tracks simultaneously but the library of playable tracks is limited by the fact that the game's creator must distribute and obtain licenses to all playable music. Even a user who has already purchased to the music must re-purchase as it is bundled with the game. Players suffer limited content and game makers can't focus on just choreography.

A segregated licensing model allows related content, like music and choreography, to be owned by separate entities but still licensed directly to the consumer without bundling.
