# Regular Expressions to Match Social Media Profiles
This repository lists regular expressions to match and extract information from URLs of social media profiles.
So if you find a hyperlink to this repo somewhere on the web, i.e. https://github.com/lorey/social-media-profiles-regexs/, 
the regular expressions in this repo allow you find out it's a Github link pointing to a repo
as well as extract the username `lorey` and the repo name `social-media-profiles-regexs` from this URL.

Features:

- detect the platform a url points to (all major platforms supported)
- extract the information contained within the url (without opening the url, of course)
- extract emails and phone numbers from hyperlinks

Please note:
If you want to extract social media links, depending on your case, there are possibly easier ways:

* I've created a [Python library called socials](https://github.com/lorey/socials) that uses these expressions to *automate url detection* and data extraction.
You input the urls, it extracts the type of platform as well as the contained information, e.g. the linked social media profiles.
* There's also a [Socials API](https://github.com/lorey/socials-api) which makes the socials python package available via REST and JSON. 
You can use it for free at [socials.karllorey.com](http://socials.karllorey.com/) or deploy it yourself.
You simply input any URL you want to extract profiles from. It will then fetch and return all social media links from the given website. 
Try it [here](http://socials.karllorey.com/try).

If you're missing a particular platform, please feel free to add it.
Also feel free to add a test that does not work.
An explanation of how this repo works can be found in [CONTRIBUTING.md](CONTRIBUTING.md).
You might also open an issue, of course, I'm happy to help!

## Table of Contents
- [angellist](#angellist)
- [crunchbase](#crunchbase)
- [discord](#discord)
- [email](#email)
- [facebook](#facebook)
- [github](#github)
- [google plus](#google-plus)
- [hackernews](#hackernews)
- [instagram](#instagram)
- [link_in_bio](#link_in_bio)
- [linkedin](#linkedin)
- [medium](#medium)
- [patreon](#patreon)
- [phone](#phone)
- [reddit](#reddit)
- [skype](#skype)
- [snapchat](#snapchat)
- [soundcloud](#soundcloud)
- [spotify](#spotify)
- [stackexchange](#stackexchange)
- [stackexchange network](#stackexchange-network)
- [stackoverflow](#stackoverflow)
- [telegram](#telegram)
- [twitter](#twitter)
- [vimeo](#vimeo)
- [xing](#xing)
- [youtube](#youtube)
- [Monster Regex](#monster-regex)



## angellist

### company
```regex
(?:https?:)?\/\/angel\.co\/company\/(?P<company>[A-z0-9_-]+)(?:\/(?P<company_subpage>[A-z0-9-]+))?
```


Examples: 

- https://angel.co/company/twitter
- https://angel.co/company/twitter/culture

### job
```regex
(?:https?:)?\/\/angel\.co\/company\/(?P<company>[A-z0-9_-]+)\/jobs\/(?P<job_permalink>(?P<job_id>[0-9]+)-(?P<job_slug>[A-z0-9-]+))
```


Examples: 

- https://angel.co/company/twitter/jobs/576275-engineering-manager

### user
```regex
(?:https?:)?\/\/angel\.co\/(?P<type>u|p)\/(?P<user>[A-z0-9_-]+)
```
There are root-level direct links to users, e.g. angel.co/karllorey, that get redirected to these new user links now. Sometimes it's /p/, sometimes it's /u/, haven't figured out why that is...

Examples: 

- https://angel.co/p/naval
- https://angel.co/u/karllorey


## crunchbase

### company
```regex
(?:https?:)?\/\/crunchbase\.com\/organization\/(?P<organization>[A-z0-9_-]+)
```


Examples: 

- http://crunchbase.com/organization/acme-corp

### person
```regex
(?:https?:)?\/\/crunchbase\.com\/person\/(?P<person>[A-z0-9_-]+)
```


Examples: 

- http://crunchbase.com/person/karl-lorey


## discord

### server_invite
```regex
^(?:https?:\/\/|\/\/)?(?:www\.)?(?:discord\.gg|discord\.com\/invite)\/(?P<code>[A-Za-z0-9-]+)\/?$
```
Matches Discord server invite URLs from discord.gg or discord.com/invite, with or without protocol or www.

Examples: 

- discord.gg/aRJmz95KWa
- http://discord.com/invite/aRJmz95KWa/
- http://discord.gg/aRJmz95KWa
- https://discord.com/invite/aRJmz95KWa
- https://discord.gg/aRJmz95KWa
- https://www.discord.gg/aRJmz95KWa
- www.discord.com/invite/aRJmz95KWa


## email

### mailto
```regex
(?:mailto:)?(?P<email>[A-z0-9_.+-]+@[A-z0-9_.-]+\.[A-z]+)
```
This matches plain emails and mailto hyperlinks. This regex is intended for scraping and not as a validation. See why: ["Your email validation logic is wrong"](https://www.netmeister.org/blog/email.html).

Examples: 

- jeff@amazon.com
- mailto:jeff@amazon.com
- mailto:plususer+test@gmail.com


## facebook

### profile
```regex
(?:https?:)?\/\/(?:www\.)?(?:facebook|fb)\.com\/(?P<profile>(?![A-z]+\.php)(?!marketplace|gaming|watch|me|messages|help|search|groups)[A-z0-9_\-\.]+)\/?
```
A profile can be a page, a user profile, or something else. Since Facebook redirects these URLs to all kinds of objects (user, pages, events, and so on), you have to verify that it's actually a user. See https://developers.facebook.com/docs/graph-api/reference/profile

Examples: 

- http://fb.com/peter_parker-miller
- https://facebook.com/peter.parker
- https://facebook.com/peterparker

### profile by id
```regex
(?:https?:)?\/\/(?:www\.)facebook.com/(?:profile.php\?id=)?(?P<id>[0-9]+)
```


Examples: 

- https://www.facebook.com/100004123456789
- https://www.facebook.com/profile.php?id=100004123456789


## github

### repo
```regex
(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<login>[A-z0-9_-]+)\/(?P<repo>[A-z0-9_-]+)\/?
```
Exclude subdomains as these redirect to github pages sometimes.

Examples: 

- https://github.com/lorey/socials

### user
```regex
(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<login>[A-z0-9_-]+)\/?
```
Exclude subdomains other than `www.` as these redirect to github pages sometimes.

Examples: 

- https://github.com/lorey/


## google plus

### user id
```regex
(?:https?:)?\/\/plus\.google\.com\/(?P<id>[0-9]{21})
```
Matches profile numbers with exactly 21 digits.

Examples: 

- https://plus.google.com/111111111111111111111

### username
```regex
(?:https?:)?\/\/plus\.google\.com\/\+(?P<username>[A-z0-9+]+)
```
Matches username.

Examples: 

- https://plus.google.com/+googleplususername


## hackernews

### item
```regex
(?:https?:)?\/\/news\.ycombinator\.com\/item\?id=(?P<item>[0-9]+)
```
An item can be a post or a direct link to a comment.

Examples: 

- https://news.ycombinator.com/item?id=23290375

### user
```regex
(?:https?:)?\/\/news\.ycombinator\.com\/user\?id=(?P<user>[A-z0-9_-]+)
```


Examples: 

- https://news.ycombinator.com/user?id=CamelCaps
- https://news.ycombinator.com/user?id=dash-and-underscore_are-valid
- https://news.ycombinator.com/user?id=lorey


## instagram

### profile
```regex
(?:https?:)?\/\/(?:www\.)?(?:instagram\.com|instagr\.am)\/(?P<username>[A-Za-z0-9_](?:(?:[A-Za-z0-9_]|(?:\.(?!\.))){0,28}(?:[A-Za-z0-9_]))?)
```
The rules:

* Matches with one . in them disco.dude but not two .. disco..dude
* Ending period not matched discodude.
* Match underscores _disco__dude
* Max characters of 30 1234567890123456789012345678901234567890

Examples: 

- https://instagram.com/__disco__dude
- https://instagram.com/disco.dude
- https://www.instagr.am/__disco__dude


## link_in_bio

### profile
```regex
^(?:https?:\/\/|\/\/)?(?:www\.)?(?:linktr\.ee|linktree\.com|beacons\.ai|bio\.fm|camps\.bio|carrd\.co|lnk\.bio|linkin\.bio|contactinbio\.com|taplink\.cc|shorby\.io|milkshake\.app|linkpop\.com|about\.me|koji\.app|url\.bio|bio\.link|ping\.bio|use1\.link|bio\.site)\/(?P<username>[A-Za-z0-9][A-Za-z0-9_-]*)\/?$
```
Matches profile pages on popular 'link in bio' platforms (e.g. Linktree, Beacons, Carrd, etc.) with optional protocol and www subdomain.

Examples: 

- about.me/johnsmith
- bio.fm/johnsmith
- bio.link/johnsmith
- bio.site/allfourmusic
- http://www.linktree.com/john_smith
- https://carrd.co/johnsmith
- https://linktr.ee/johnsmith
- koji.app/john_smith
- milkshake.app/johnsmith
- ping.bio/johnsmith
- shorby.io/johnsmith
- url.bio/johnsmith
- use1.link/AudibleGenius
- www.beacons.ai/john-smith
- www.bio.site/allfourmusic


## linkedin

### company
```regex
(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/(?P<company_type>(company)|(school))\/(?P<company_permalink>[A-z0-9-À-ÿ\.]+)\/?
```
This matches companies and schools. Permalink is an integer id or a slug. The id permalinks redirect to the slug permalinks as soon as one is set. Permalinks can contain special characters. Recently, company links that are actually schools get redirected to newly introduced /school/ permalinks, see the university example below.

Examples: 

- https://fr.linkedin.com/school/université-grenoble-alpes/
- https://linkedin.com/company/dash-company.io
- https://www.linkedin.com/company/1234567/

### post
```regex
(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/feed\/update\/urn:li:activity:(?P<activity_id>[0-9]+)\/?
```
Direct link to a Linkedin post, only contains a post id.

Examples: 

- https://www.linkedin.com/feed/update/urn:li:activity:6665508550111912345/

### profile
```regex
(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/in\/(?P<permalink>[\w\-\_À-ÿ%]+)\/?
```
These are the currently used, most-common urls ending in /in/<permalink>

Examples: 

- https://de.linkedin.com/in/peter-müller-81a8/
- https://linkedin.com/in/karllorey

### profile_pub
```regex
(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/pub\/(?P<permalink_pub>[A-z0-9_-]+)(?:\/[A-z0-9]+){3}\/?
```
These are old public urls not used anymore, more info at [quora](https://www.quora.com/What-is-the-difference-between-www-linkedin-com-pub-and-www-linkedin-com-in)

Examples: 

- https://linkedin.com/pub/karllorey/abc/123/be
- https://www.linkedin.com/pub/karllorey/abc/123/be


## medium

### post
```regex
(?:https?:)?\/\/medium\.com\/(?:(?:@(?P<username>[A-z0-9]+))|(?P<publication>[a-z-]+))\/(?P<slug>[a-z0-9\-]+)-(?P<post_id>[A-z0-9]+)(?:\?.*)?
```


Examples: 

- https://medium.com/@karllorey/keeping-pandas-dataframes-clean-when-importing-json-348d3439ed67
- https://medium.com/does-exist/some-post-123abc

### post of subdomain publication
```regex
(?:https?:)?\/\/(?P<publication>(?!www)[a-z-]+)\.medium\.com\/(?P<slug>[a-z0-9\-]+)-(?P<post_id>[A-z0-9]+)(?:\?.*)?
```
Can't match these with the regular post regex as redefinitions of subgroups are not allowed in pythons regex.

Examples: 

- https://onezero.medium.com/what-facebooks-remote-work-policy-means-for-the-future-of-tech-salaries-everywhere-edf859226b62?source=grid_home------

### user
```regex
(?:https?:)?\/\/medium\.com\/@(?P<username>[A-z0-9]+)(?:\?.*)?
```


Examples: 

- https://medium.com/@karllorey

### user by id
```regex
(?:https?:)?\/\/medium\.com\/u\/(?P<user_id>[A-z0-9]+)(?:\?.*)
```
Now redirects to new user profiles. Follow with a head or get request.

Examples: 

- https://medium.com/u/b3d3d3653c2c?source=post_page-----da92b81b85ef----------------------


## patreon

### profile
```regex
^(?:https?:\/\/|\/\/)?(?:www\.)?patreon\.com\/(?:join\/)?(?P<username>(?!posts\b|login\b|signup\b|discover\b|messages\b|home\b|activity\b|settings\b|faq\b|about\b|policy\b|apps\b|support\b|news\b|blog\b|podcast\b|press\b|careers\b|search\b|join\b)[A-Za-z0-9_-]+)\/?$
```
Matches Patreon user profile URLs, including /join/username, and excludes non-profile paths like /login or /posts.

Examples: 

- http://patreon.com/join/mkbhd
- https://patreon.com/join/mkbhd/
- https://patreon.com/mkbhd
- https://www.patreon.com/join/mkbhd
- https://www.patreon.com/mkbhd


## phone

### phone number
```regex
(?:tel|phone|mobile):(?P<number>\+?[0-9. -]+)
```
Should be cleaned afterwards to strip dots, spaces, etc.

Examples: 

- tel:+49 900 123456
- tel:+49900123456


## reddit

### user
```regex
(?:https?:)?\/\/(?:[a-z]+\.)?reddit\.com\/(?:u(?:ser)?)\/(?P<username>[A-z0-9\-\_]*)\/?
```


Examples: 

- https://old.reddit.com/user/ar-guetita
- https://reddit.com/u/ar-guetita


## skype

### profile
```regex
(?:(?:callto|skype):)(?P<username>[a-z][a-z0-9\.,\-_]{5,31})(?:\?(?:add|call|chat|sendfile|userinfo))?
```
Matches Skype's URLs to add contact, call, chat. More info at [Skype SDK's docs](https://docs.microsoft.com/en-us/skype-sdk/skypeuris/skypeuris).

Examples: 

- skype:echo123
- skype:echo123?call


## snapchat

### profile
```regex
(?:https?:)?\/\/(?:www\.)?snapchat\.com\/add\/(?P<username>[A-z0-9\.\_\-]+)\/?
```


Examples: 

- https://www.snapchat.com/add/peterparker


## soundcloud

### player
```regex
(?:https?:)?\/\/w\.soundcloud\.com\/player\/\?(?:[^\s]*?&)?url=https%3A%2F%2Fapi\.soundcloud\.com%2F(?P<type>tracks|playlists)%2F(?P<id>[0-9]+)(?:[&\?#][^\s]*)?
```
Matches SoundCloud embedded player URLs, pointing to tracks or playlists via decoded API URLs inside the url= param.

Examples: 

- https://w.soundcloud.com/player/?url=https%3A%2F%2Fapi.soundcloud.com%2Fplaylists%2F331919427&visual=true
- https://w.soundcloud.com/player/?visual=true&url=https%3A%2F%2Fapi.soundcloud.com%2Ftracks%2F2046431760&show_artwork=true&maxheight=80&maxwidth=640

### playlist
```regex
(?:https?:)?\/\/(?:www\.|m\.)?soundcloud\.com\/(?P<artist>[A-Za-z0-9_.-]+)\/sets\/(?P<playlist>[A-Za-z0-9_.-]+)\/?
```
Matches SoundCloud playlist URLs. Playlists are under /<artist>/sets/<slug> with optional subdomains and trailing slash.

Examples: 

- https://m.soundcloud.com/foreromusic/sets/dreamscapes/
- https://soundcloud.com/foreromusic/sets/dreamscapes
- https://www.soundcloud.com/foreromusic/sets/dreamscapes

### profile
```regex
(?:https?:)?\/\/(?:www\.|m\.)?soundcloud\.com\/(?!oembed\/?$)(?P<username>[A-Za-z0-9_.-]+)\/?
```
Matches SoundCloud user profile URLs with optional www. or m. subdomains, excluding the oembed endpoint.

Examples: 

- https://m.soundcloud.com/foreromusic
- https://soundcloud.com/foreromusic
- https://soundcloud.com/foreromusic/
- https://www.soundcloud.com/foreromusic
- https://www.soundcloud.com/foreromusic/

### redirect
```regex
(?:https?:)?\/\/(?:on\.soundcloud\.com|soundcloud\.app\.goo\.gl)\/(?P<token>[A-Za-z0-9]{5,25})\/?
```
SoundCloud short redirects to canonical track/playlist/profile URLs. Tokens are opaque; use Location header for canonical URL resolution.

Examples: 

- https://on.soundcloud.com/w9Uvv666ksyKCFto9
- https://soundcloud.app.goo.gl/a1b2C

### track
```regex
(?:https?:)?\/\/(?:www\.|m\.)?soundcloud\.com\/(?P<artist>[A-Za-z0-9_.-]+)\/(?P<track>[A-Za-z0-9_.-]+)(?:\/s-(?P<secret>[A-Za-z0-9]+))?\/?
```
Matches SoundCloud track URLs with optional www. or m. subdomains and optional secret /s-XXX suffix.

Examples: 

- https://m.soundcloud.com/asrilos/symphony-of-light
- https://soundcloud.com/cade-turner/cade-turner-symphony-of-light
- https://soundcloud.com/foreromusic/the-secret-track/s-AbCdEf123
- https://www.soundcloud.com/foreromusic/track-name/


## spotify

### artist
```regex
^(?:https?:\/\/|\/\/)?(?:open\.)?spotify\.com\/artist\/(?P<id>[A-Za-z0-9]{22})(?:\?.*)?$|^spotify:artist:(?P<uri_id>[A-Za-z0-9]{22})$
```
Matches Spotify artist profile URLs and URIs

Examples: 

- http://open.spotify.com/artist/1vCWHaC5f2uS3yhpwWbIA6
- https://open.spotify.com/artist/1vCWHaC5f2uS3yhpwWbIA6
- https://open.spotify.com/artist/1vCWHaC5f2uS3yhpwWbIA6?si=dummycode&utm_source=whoknows
- open.spotify.com/artist/1vCWHaC5f2uS3yhpwWbIA6
- spotify:artist:1vCWHaC5f2uS3yhpwWbIA6

### playlist
```regex
^(?:https?:\/\/|\/\/)?(?:open\.)?spotify\.com\/playlist\/(?P<id>[A-Za-z0-9]{22})(?:\?.*)?$|^spotify:playlist:(?P<uri_id>[A-Za-z0-9]{22})$
```
Matches Spotify playlist URLs and URIs.

Examples: 

- //open.spotify.com/playlist/37i9dQZF1DXcBWIGoYBM5M?si=xyz
- http://open.spotify.com/playlist/37i9dQZF1DXcBWIGoYBM5M
- https://open.spotify.com/playlist/2JWoC2BRoUOHsPjcgxMIyk?si=75e79774dcdd481f&nd=1&dlsi=abeb6d548f2c4713
- https://open.spotify.com/playlist/37i9dQZF1DXcBWIGoYBM5M
- spotify:playlist:37i9dQZF1DXcBWIGoYBM5M


## stackexchange

### user
```regex
(?:https?:)?\/\/(?:www\.)?stackexchange\.com\/users\/(?P<id>[0-9]+)\/(?P<username>[A-z0-9-_.]+)\/?
```
This is the meta-platform above stackoverflow, etc. Username can be changed at any time, user_id is persistent.

Examples: 

- https://stackexchange.com/users/12345/lorey


## stackexchange network

### user
```regex
(?:https?:)?\/\/(?:(?P<community>[a-z]+(?!www))\.)?stackexchange\.com\/users\/(?P<id>[0-9]+)\/(?P<username>[A-z0-9-_.]+)\/?
```
While there are some "named" communities in the stackexchange network like stackoverflow, many only exist as subdomains, i.e. gaming.stackexchange.com. Again, username can be changed at any time, user_id is persistent.

Examples: 

- https://gaming.stackexchange.com/users/12345/lorey


## stackoverflow

### question
```regex
(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/questions\/(?P<id>[0-9]+)\/(?P<title>[A-z0-9-_.]+)\/?
```


Examples: 

- https://stackoverflow.com/questions/12345/how-to-embed

### user
```regex
(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/users\/(?P<id>[0-9]+)\/(?P<username>[A-z0-9-_.]+)\/?
```
Username can be changed at any time, user_id is persistent.

Examples: 

- https://stackoverflow.com/users/12345/lorey


## telegram

### profile
```regex
(?:https?:)?\/\/(?:t(?:elegram)?\.me|telegram\.org)\/(?P<username>[a-z0-9\_]{5,32})\/?
```
Matches for t.me, telegram.me and telegram.org.

Examples: 

- https://t.me/peterparker


## twitter

### status
```regex
^(?:https?:\/\/|\/\/)?(?:www\.)?(?:twitter\.com|x\.com)\/@?(?P<username>[A-Za-z0-9_]+)\/status\/(?P<tweet_id>[0-9]+)\/?$
```
Matches tweets on twitter.com or x.com including optional @ prefix on username.

Examples: 

- https://twitter.com/karllorey/status/1259924082067374088
- https://www.x.com/karllorey/status/1259924082067374088/
- https://x.com/karllorey/status/1259924082067374088
- x.com/@karllorey/status/1259924082067374088

### user
```regex
^(?:https?:\/\/|\/\/)?(?:www\.)?(?:twitter\.com|x\.com)\/(?:(?:@?(?P<username>(?!home$|share$|privacy$|tos$)[A-Za-z0-9_]+))|intent\/(?:user|follow)\?(?:[^#?&=]+=[^#?&=]*&)*(?:screen_name=(?P<screen_name>[A-Za-z0-9_]+)|user_id=(?P<user_id>[0-9]+))(?:&[^#]*)*)\/?(?:[?#].*)?$
```
Matches Twitter/X profiles via /@username, /username, and intent links with screen_name or user_id. Only public user profile URLs.

Examples: 

- https://twitter.com/@karllorey
- https://twitter.com/intent/user?ref=xyz&screen_name=NASA&src=twsrc
- https://twitter.com/intent/user?screen_name=NASA
- https://twitter.com/intent/user?src=twsrc&user_id=3308337&ref=abc
- https://twitter.com/intent/user?user_id=3308337
- https://twitter.com/karllorey
- https://x.com/karllorey


## vimeo

### user
```regex
(?:https?:)?\/\/vimeo\.com\/user(?P<id>[0-9]+)
```


Examples: 

- https://vimeo.com/user46726126

### video
```regex
(?:https?:)?\/\/(?:(?:www)?vimeo\.com|player.vimeo.com\/video)\/(?P<id>[0-9]+)
```


Examples: 

- https://player.vimeo.com/video/148751763
- https://vimeo.com/148751763


## xing

### profile
```regex
(?:https?:)?\/\/(?:www\.)?xing.com\/profile\/(?P<slug>[A-z0-9-\_]+)
```
Default slugs are Firstname_Lastname. If several people with the same name exist, a number is appended.

Examples: 

- https://www.xing.com/profile/Tobias_Zilbersahn5


## youtube

### channel
```regex
^(?:https?:)?\/\/(?:www\.)?(?:youtube\.com\/(?:channel\/(?P<id>[A-Za-z0-9_-]+)|c\/(?P<custom>[A-Za-z0-9_-]+)|@?(?P<handle>[A-Za-z0-9_-]+)))(?:\/videos)?\/?$
```


Examples: 

- https://www.youtube.com/@JPPGmbH
- https://www.youtube.com/c/JPPGmbH
- https://www.youtube.com/c/JPPGmbH/videos
- https://www.youtube.com/channel/UC3y00Z1zFPc-8Z9xg8ydC-A
- https://www.youtube.com/channel/UCtAh1m085QkEKYNg0j_6r8A/videos

### user
```regex
(?:https?:)?\/\/(?:[A-z]+\.)?youtube.com\/user\/(?P<username>[A-z0-9]+)\/?
```


Examples: 

- https://www.youtube.com/user/JPPGmbH

### video
```regex
(?:https?:)?\/\/(?:(?:www\.)?youtube\.com\/(?:watch\?v=|embed\/)|youtu\.be\/)(?P<id>[A-z0-9\-\_]+)
```
Matches youtube video links like https://www.youtube.com/watch?v=dQw4w9WgXcQ and shortlinks like https://youtu.be/dQw4w9WgXcQ

Examples: 

- https://www.youtube.com/watch?v=dQw4w9WgXcQ
- https://youtu.be/dQw4w9WgXcQ
- https://youtube.com/embed/dQw4w9WgXcQ
- https://youtube.com/watch?v=6_b7RDuLwcI

## Monster Regex
If you want to match and extract the data from all urls with one regex, use this monster.
It will return the data for all the platforms above.
The regex subgroups are prefixed with the platform, 
e.g. `angellist__company` instead of just `company` in the angellist company regex, 
as some regex implementations don't support defining subgroups more than once which would introduce errors if  the same subgroup name is used in two or more platforms.

```regex
(?P<angellist__company>(?:https?:)?\/\/angel\.co\/company\/(?P<angellist__company__company>[A-z0-9_-]+)(?:\/(?P<angellist__company__company_subpage>[A-z0-9-]+))?)|(?P<angellist__job>(?:https?:)?\/\/angel\.co\/company\/(?P<angellist__job__company>[A-z0-9_-]+)\/jobs\/(?P<angellist__job__job_permalink>(?P<angellist__job__job_id>[0-9]+)-(?P<angellist__job__job_slug>[A-z0-9-]+)))|(?P<angellist__user>(?:https?:)?\/\/angel\.co\/(?P<angellist__user__type>u|p)\/(?P<angellist__user__user>[A-z0-9_-]+))|(?P<crunchbase__company>(?:https?:)?\/\/crunchbase\.com\/organization\/(?P<crunchbase__company__organization>[A-z0-9_-]+))|(?P<crunchbase__person>(?:https?:)?\/\/crunchbase\.com\/person\/(?P<crunchbase__person__person>[A-z0-9_-]+))|(?P<discord__server_invite>^(?:https?:\/\/|\/\/)?(?:www\.)?(?:discord\.gg|discord\.com\/invite)\/(?P<discord__server_invite__code>[A-Za-z0-9-]+)\/?$)|(?P<email__mailto>(?:mailto:)?(?P<email__mailto__email>[A-z0-9_.+-]+@[A-z0-9_.-]+\.[A-z]+))|(?P<facebook__profile>(?:https?:)?\/\/(?:www\.)?(?:facebook|fb)\.com\/(?P<facebook__profile__profile>(?![A-z]+\.php)(?!marketplace|gaming|watch|me|messages|help|search|groups)[A-z0-9_\-\.]+)\/?)|(?P<facebook__profile_by_id>(?:https?:)?\/\/(?:www\.)facebook.com/(?:profile.php\?id=)?(?P<facebook__profile_by_id__id>[0-9]+))|(?P<github__repo>(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<github__repo__login>[A-z0-9_-]+)\/(?P<github__repo__repo>[A-z0-9_-]+)\/?)|(?P<github__user>(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<github__user__login>[A-z0-9_-]+)\/?)|(?P<google_plus__user_id>(?:https?:)?\/\/plus\.google\.com\/(?P<google_plus__user_id__id>[0-9]{21}))|(?P<google_plus__username>(?:https?:)?\/\/plus\.google\.com\/\+(?P<google_plus__username__username>[A-z0-9+]+))|(?P<hackernews__item>(?:https?:)?\/\/news\.ycombinator\.com\/item\?id=(?P<hackernews__item__item>[0-9]+))|(?P<hackernews__user>(?:https?:)?\/\/news\.ycombinator\.com\/user\?id=(?P<hackernews__user__user>[A-z0-9_-]+))|(?P<instagram__profile>(?:https?:)?\/\/(?:www\.)?(?:instagram\.com|instagr\.am)\/(?P<instagram__profile__username>[A-Za-z0-9_](?:(?:[A-Za-z0-9_]|(?:\.(?!\.))){0,28}(?:[A-Za-z0-9_]))?))|(?P<link_in_bio__profile>^(?:https?:\/\/|\/\/)?(?:www\.)?(?:linktr\.ee|linktree\.com|beacons\.ai|bio\.fm|camps\.bio|carrd\.co|lnk\.bio|linkin\.bio|contactinbio\.com|taplink\.cc|shorby\.io|milkshake\.app|linkpop\.com|about\.me|koji\.app|url\.bio|bio\.link|ping\.bio|use1\.link|bio\.site)\/(?P<link_in_bio__profile__username>[A-Za-z0-9][A-Za-z0-9_-]*)\/?$)|(?P<linkedin__company>(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/(?P<linkedin__company__company_type>(company)|(school))\/(?P<linkedin__company__company_permalink>[A-z0-9-À-ÿ\.]+)\/?)|(?P<linkedin__post>(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/feed\/update\/urn:li:activity:(?P<linkedin__post__activity_id>[0-9]+)\/?)|(?P<linkedin__profile>(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/in\/(?P<linkedin__profile__permalink>[\w\-\_À-ÿ%]+)\/?)|(?P<linkedin__profile_pub>(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/pub\/(?P<linkedin__profile_pub__permalink_pub>[A-z0-9_-]+)(?:\/[A-z0-9]+){3}\/?)|(?P<medium__post>(?:https?:)?\/\/medium\.com\/(?:(?:@(?P<medium__post__username>[A-z0-9]+))|(?P<medium__post__publication>[a-z-]+))\/(?P<medium__post__slug>[a-z0-9\-]+)-(?P<medium__post__post_id>[A-z0-9]+)(?:\?.*)?)|(?P<medium__post_of_subdomain_publication>(?:https?:)?\/\/(?P<medium__post_of_subdomain_publication__publication>(?!www)[a-z-]+)\.medium\.com\/(?P<medium__post_of_subdomain_publication__slug>[a-z0-9\-]+)-(?P<medium__post_of_subdomain_publication__post_id>[A-z0-9]+)(?:\?.*)?)|(?P<medium__user>(?:https?:)?\/\/medium\.com\/@(?P<medium__user__username>[A-z0-9]+)(?:\?.*)?)|(?P<medium__user_by_id>(?:https?:)?\/\/medium\.com\/u\/(?P<medium__user_by_id__user_id>[A-z0-9]+)(?:\?.*))|(?P<patreon__profile>^(?:https?:\/\/|\/\/)?(?:www\.)?patreon\.com\/(?:join\/)?(?P<patreon__profile__username>(?!posts\b|login\b|signup\b|discover\b|messages\b|home\b|activity\b|settings\b|faq\b|about\b|policy\b|apps\b|support\b|news\b|blog\b|podcast\b|press\b|careers\b|search\b|join\b)[A-Za-z0-9_-]+)\/?$)|(?P<phone__phone_number>(?:tel|phone|mobile):(?P<phone__phone_number__number>\+?[0-9. -]+))|(?P<reddit__user>(?:https?:)?\/\/(?:[a-z]+\.)?reddit\.com\/(?:u(?:ser)?)\/(?P<reddit__user__username>[A-z0-9\-\_]*)\/?)|(?P<skype__profile>(?:(?:callto|skype):)(?P<skype__profile__username>[a-z][a-z0-9\.,\-_]{5,31})(?:\?(?:add|call|chat|sendfile|userinfo))?)|(?P<snapchat__profile>(?:https?:)?\/\/(?:www\.)?snapchat\.com\/add\/(?P<snapchat__profile__username>[A-z0-9\.\_\-]+)\/?)|(?P<soundcloud__player>(?:https?:)?\/\/w\.soundcloud\.com\/player\/\?(?:[^\s]*?&)?url=https%3A%2F%2Fapi\.soundcloud\.com%2F(?P<soundcloud__player__type>tracks|playlists)%2F(?P<soundcloud__player__id>[0-9]+)(?:[&\?#][^\s]*)?)|(?P<soundcloud__playlist>(?:https?:)?\/\/(?:www\.|m\.)?soundcloud\.com\/(?P<soundcloud__playlist__artist>[A-Za-z0-9_.-]+)\/sets\/(?P<soundcloud__playlist__playlist>[A-Za-z0-9_.-]+)\/?)|(?P<soundcloud__profile>(?:https?:)?\/\/(?:www\.|m\.)?soundcloud\.com\/(?!oembed\/?$)(?P<soundcloud__profile__username>[A-Za-z0-9_.-]+)\/?)|(?P<soundcloud__redirect>(?:https?:)?\/\/(?:on\.soundcloud\.com|soundcloud\.app\.goo\.gl)\/(?P<soundcloud__redirect__token>[A-Za-z0-9]{5,25})\/?)|(?P<soundcloud__track>(?:https?:)?\/\/(?:www\.|m\.)?soundcloud\.com\/(?P<soundcloud__track__artist>[A-Za-z0-9_.-]+)\/(?P<soundcloud__track__track>[A-Za-z0-9_.-]+)(?:\/s-(?P<soundcloud__track__secret>[A-Za-z0-9]+))?\/?)|(?P<spotify__artist>^(?:https?:\/\/|\/\/)?(?:open\.)?spotify\.com\/artist\/(?P<spotify__artist__id>[A-Za-z0-9]{22})(?:\?.*)?$|^spotify:artist:(?P<spotify__artist__uri_id>[A-Za-z0-9]{22})$)|(?P<spotify__playlist>^(?:https?:\/\/|\/\/)?(?:open\.)?spotify\.com\/playlist\/(?P<spotify__playlist__id>[A-Za-z0-9]{22})(?:\?.*)?$|^spotify:playlist:(?P<spotify__playlist__uri_id>[A-Za-z0-9]{22})$)|(?P<stackexchange__user>(?:https?:)?\/\/(?:www\.)?stackexchange\.com\/users\/(?P<stackexchange__user__id>[0-9]+)\/(?P<stackexchange__user__username>[A-z0-9-_.]+)\/?)|(?P<stackexchange_network__user>(?:https?:)?\/\/(?:(?P<stackexchange_network__user__community>[a-z]+(?!www))\.)?stackexchange\.com\/users\/(?P<stackexchange_network__user__id>[0-9]+)\/(?P<stackexchange_network__user__username>[A-z0-9-_.]+)\/?)|(?P<stackoverflow__question>(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/questions\/(?P<stackoverflow__question__id>[0-9]+)\/(?P<stackoverflow__question__title>[A-z0-9-_.]+)\/?)|(?P<stackoverflow__user>(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/users\/(?P<stackoverflow__user__id>[0-9]+)\/(?P<stackoverflow__user__username>[A-z0-9-_.]+)\/?)|(?P<telegram__profile>(?:https?:)?\/\/(?:t(?:elegram)?\.me|telegram\.org)\/(?P<telegram__profile__username>[a-z0-9\_]{5,32})\/?)|(?P<twitter__status>^(?:https?:\/\/|\/\/)?(?:www\.)?(?:twitter\.com|x\.com)\/@?(?P<twitter__status__username>[A-Za-z0-9_]+)\/status\/(?P<twitter__status__tweet_id>[0-9]+)\/?$)|(?P<twitter__user>^(?:https?:\/\/|\/\/)?(?:www\.)?(?:twitter\.com|x\.com)\/(?:(?:@?(?P<twitter__user__username>(?!home$|share$|privacy$|tos$)[A-Za-z0-9_]+))|intent\/(?:user|follow)\?(?:[^#?&=]+=[^#?&=]*&)*(?:screen_name=(?P<twitter__user__screen_name>[A-Za-z0-9_]+)|user_id=(?P<twitter__user__user_id>[0-9]+))(?:&[^#]*)*)\/?(?:[?#].*)?$)|(?P<vimeo__user>(?:https?:)?\/\/vimeo\.com\/user(?P<vimeo__user__id>[0-9]+))|(?P<vimeo__video>(?:https?:)?\/\/(?:(?:www)?vimeo\.com|player.vimeo.com\/video)\/(?P<vimeo__video__id>[0-9]+))|(?P<xing__profile>(?:https?:)?\/\/(?:www\.)?xing.com\/profile\/(?P<xing__profile__slug>[A-z0-9-\_]+))|(?P<youtube__channel>^(?:https?:)?\/\/(?:www\.)?(?:youtube\.com\/(?:channel\/(?P<youtube__channel__id>[A-Za-z0-9_-]+)|c\/(?P<youtube__channel__custom>[A-Za-z0-9_-]+)|@?(?P<youtube__channel__handle>[A-Za-z0-9_-]+)))(?:\/videos)?\/?$)|(?P<youtube__user>(?:https?:)?\/\/(?:[A-z]+\.)?youtube.com\/user\/(?P<youtube__user__username>[A-z0-9]+)\/?)|(?P<youtube__video>(?:https?:)?\/\/(?:(?:www\.)?youtube\.com\/(?:watch\?v=|embed\/)|youtu\.be\/)(?P<youtube__video__id>[A-z0-9\-\_]+))

```
