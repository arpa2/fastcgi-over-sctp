FastCGI over SCTP
=================

Many websites run from a frontend, or even just a proxy, that addresses a backend for
dynamic portions.  This is done with protocols like FastCGI; variations to this theme
exist.

The project demonstrates the virtue of running such backend connections over SCTP,
rather than TCP.  This is especially beneficial for long-distance connections between
a frontend and backend, as would arise for the plugin webmodules that ARPA2 aims for.

This project produces measurements, and will (at some point) hold code to make such
backend connections.  Interestingly, the FastCGI logic needs no change; the move to
SCTP is a drop-in replacement as far as the backend servers are concerned, they
merely require another library.

For frontends, a bit more work is needed.  The most influential aspect is that a
single connection is being shared, and that good use is made of SCTP's ability to
send frames without enforced order between them.  A bit of clever logic is required
to do this well.

Details on http://research.arpa2.org/projects/2014-sctp-fastcgi.html
