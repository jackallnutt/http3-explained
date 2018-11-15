# Alt-svc

The alternate service (Alt-svc:) header and its corresponding `ALT-SVC` HTTP/2
frame are not specifically created for QUIC. They're part of an already
designed and created mechanism for a server to tell a client: *"look, I run
the same service on THIS HOST using THIS PROTOCOL on THIS PORT"*. See details
in [RFC 7838](https://tools.ietf.org/html/rfc7838).

A client that receives such an Alt-svc response is then adviced to, if it
supports and wants to, connect to that given other host in parallel in the
background - using the specified protocol - and if it successful switch its
operations over to that instead of the initial connection.

If the initial connection uses HTTP/2 or even HTTP/1, the server can respond
and tell the client that it can connect back and try HTTP/3. It could be to
the same host or to another one that knows how to serve that origin. The
information given in such an Alt-svc response has an expiry timer making
clients will information that for a period of time so that subsequent
connections and requests can go directly to the alternative host using the
suggested alternative protocol.