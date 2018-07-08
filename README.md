# crystal json-socket [![Build Status](https://travis-ci.org/foi/crystal-json-socket.svg?branch=master)](https://travis-ci.org/foi/crystal-json-socket)

JSON-socket client & server implementation. Inspired by and wish for compatability with  [sebastianseilund/node-json-socket](https://github.com/sebastianseilund/node-json-socket/)

## Installation

Add this to your application's `shard.yml`:
```
dependencies:
  json-socket:
    github: foi/crystal-json-socket
```

## Usage

server.cr
```
require "json-socket"
server = JSONSocket::Server.new("localhost", 1234) # OR JSONSocket::Server.new(unix_socket: "/tmp/json-socket-server.sock", delimeter: "µ")
server.listen do |message, socket|
  puts message # JSON::Any # => { "test" => 1 }
  server.send_end_message(socket, { :status => "success" })
end
```
  client.cr
```
require "json-socket"
to_server = JSONSocket::Client.new("localhost", 1234) # OR JSONSocket::Client.new(unix_socket: "/tmp/json-socket-server.sock", delimeter: "µ")
result = to_server.send({ :test => 1 })
if result
  puts result["status"] # success
end
```
