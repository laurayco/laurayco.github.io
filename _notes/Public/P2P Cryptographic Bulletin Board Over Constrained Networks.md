---
title: P2P Cryptographic Bulletin Board Over Constrained Networks
feed: show
date: 2022-12-19
---

# Scenario:
You want to have a web forum which is private to a specific group of people. You don't know how many people will be in this group, and it may grow or shrink over time. You don't want to rely on a third party to host your forum data, and you don't want to rely on the internet to send this data because P2P is difficult over the internet.

# Proposal:
1. Every person keeps a profile. This profile has a collection of identities.
	1. Each identity belongs to at most one group
	2. Each identity has an associated RSA key pair
	3. Each identity chooses what meta-data to share from the individual's profile
2. Every person maintains an address book.
	1. This is essentially a copy of other people's profiles, with public keys only.
	2. Identities are filled out during discovery phase of joining a group, and associated with said group.
		1. Linking two identities together will establish a "contact"
			1. "Contacts" are just an organizational unit so that it's more obvious when one identity in group A is the same person as an identity in group B.
3. Groups are just a cryptographically stored / shared address book. A group will have a PSK which is used to encrypt all communications within the group. All communications should also include a header which includes the thumbprint and signature of the message body from the identity which authored the communication.
	1. Communications can be text, binary, or meta
	2. text communications are just utf-8 strings (can be interpreted as markdown, for example)
	3. binary communications are raw bytes, and should include an additional header indicating a filename
	4. meta communications will pertain to group membership and carrier information:
		1. group identification 
		2. new member introduction
		3. member dismissal proposal
		4. use of a trusted internet courier
		5. votes
			1. options: allow (no re-key), allow (re-key), reject
			2. note: re-key implies that if the vote passes, a new key should be calculated for future communications.
4. An "envelope" is a container which includes one or more communications.
5. A "carrier" is a method through which an envelope may be transmitted to other group members, eg:
	1. Digital File: the crypto bulletin software leaves transmitting a digital file to the users discretion (can be sent over eg: email, signal, slack, NAS, twitter threads as base64 dumps)
	2. Trusted Internet Courier: HTTP(S) transport through a trusted server on a common network (usually internet).
	3. Close proximity exchanges, eg: hypersonic networking, airdrop(?) or "nearby share", bluetooth(?), LAN
	4. OpenPGP email
	5. Beacons: for particularly small communications, a "beacon" could be used (think QR Code displayed on a public place or NFC tag placed down.) The storage available in these cases is extremely constrained (<1KB for most NFC tags, and data density of QR codes is not too great either, expect no more than 3KB.)
		1. As a supplement to this, Beacons can be used to link to a digital envelope file location. This would save space, requiring only a header indicating what the beacon is (think "magic numbers" which mean "crypto bulletin board relay beacon"), what group it belongs to and then a link, which should either serve the digital envelope file itself or a 301 redirect to a url that will.

# Motivations: or, why the hell would you want this?
Recent history makes me doubt that society can be relied on to remain stable. In today's political climate, being able to communicate with trusted communities is vital and equally vital is that untrusted parties not be privy to such information. Terrorist attacks on power infrastructure, cyber attacks on AWS, natural disasters, etc are all threats to the stability of internet communications and I think having alternative methods of distribution are necessary. In short: I think generally people will have their phones and be able to keep them powered, for the most part but anything beyond that I find less certain. This solution outlines ideas for an E2E encrypted bulletin board shared over sneakernet - if this is not private nor fault tolerant then I do not believe such concepts are achievable.