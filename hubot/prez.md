%title: Hubot - Kezako?
%author: masterzen
%date: 2017-08-10





-> Hubot <-
===========

-------------------------------------------------
-> # CHAT ROBOT <-

* from fine folks at Github
* written in coffeescript
* tons of (not working) plugins
* connects to chat services (slack, campfire, 
hipchat, irc...)

-------------------------------------------------
-> # CHATOPS <-

Perform ops work directly in the chat:

* allow people to be trained by seeing others
* 1 place for everything (reduces stress during incident)
* allows permanent auditing

-------------------------------------------------
-> # DEMO <-

* simple fun things:
 `image me`, `flip table`
* Grafana or datadog:
`graph -1d avg:api.http.request.total.response_time.count{*}`
* jenkins integration 
`jenkins build list`
* github integration 
`show prs team:Scala`

-------------------------------------------------
-> # WANNA TRY URSELF <-

* use the sandbox room
* or speak to hipchat directly

-------------------------------------------------
-> # LOOKING INSIDE <-

* plugins are coffeescript callbacks
* triggered by:
  * commands
  * hearings

-------------------------------------------------
-> # COMMANDS <-

~~~
robot.respond /is it beer time\s*\?/i, (res) ->
  res.reply "I'm thirsty!"
  return
~~~

-------------------------------------------------
-> # HEARINGS <-

~~~
robot.hear /I like pie/i, (res) ->
  res.emote "makes a freshly baked pie"
  return
~~~

-------------------------------------------------
-> # RESPONSE <-

* reply: reply to the user that issued the command
* send: write to the room the order came from
* emote: use hipchat /me

-------------------------------------------------
-> # HTTP <-

GET
~~~
 robot.http("https://website")
    .get() (err, res, body) ->
      # add your code
~~~
POST/PUT possible, json...
scraping with 'cheerio'

-------------------------------------------------
-> # MY BRAIN HURTS <-

hubot has a persistent brain (redis based)
~~~
saidInsults = robot.brain.get('saidInsults')
robot.brain.set 'saidInsults', saidInsults+1
~~~

-------------------------------------------------
-> # A VERY SIMPLE EXAMPLE <-

~~~
module.exports = (robot) ->
  robot.respond /b64 encode( me)? (.*)/i, (msg) ->
    msg.send new Buffer(msg.match[2]).toString('base64')
~~~

-------------------------------------------------
-> # DEV <-

* test locally with `./bin/hubot`

-------------------------------------------------
-> # DEPLOYMENT <-

* our hubot is on heroku
* `git push heroku master`
(you need the key)
* `heroku logs`
(you need an heroku account)

-------------------------------------------------
-> # LIVECODING! <-




-> we need a very simple idea




-------------------------------------------------




-> ?? QUESTIONS ?? <-







