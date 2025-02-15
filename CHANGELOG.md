Changelog
=========

## [1.34.4] - 2024-06-26
### Fixed

 * fix getSysConn to work with TLS (#918)

### Changed

 * Switch to aliases for Go versions in CI (#919)

## [1.34.3] - 2024-04-23
### Fixed

 * Fix a DoS vulnerability of the vendored apache-thrift library (#915, #916)

## [1.34.2] - 2024-02-16
### Added

 * Expose `inbound.cancels.{requested,honored}` metrics (#912)

## [1.34.1] - 2023-12-11
### Fixed

 * Fix unknown error type in span tag rpc.tchannel.system_error_code (#907)

## [1.34.0] - 2023-10-17

### Added

* Emit the error code and type to the tracing span for inbound calls (#903)

### Changed

 * Update go.mod and github test to go 1.21 (#899)

## [1.33.0] - 2023-03-20

### Added

 * Optionally send cancelled frames when context is canceled (#890)

### Changed

 * Update dependencies as per recommendations (#894)
 * Test against Go 1.19 and 1.20 (#892)

## [1.32.1] - 2022-08-23
### Fixed

 * Release unsent frames when flushing fragments (#887)

## [1.32.0] - 2022-07-12
### Changed
 * Add TLS option in testutils.NewServerChannel (#882)

## [1.31.0] - 2022-05-04
### Changed
 * thrift-gen going to use vendored apache-thrift code. Currently vendored apache-thrift pinned to b2a4d4ae21c789b689dd162deb819665567f481c.

## [1.22.3] - 2022-03-28
### Changed
 * Fix memory leak due to unreturned frames in the relayer.
 * Test against Go 1.17 and 1.18 in CI.
 * Migrate to go mod.

## [1.22.2] - 2021-11-10
### Changed
 * Fixes related to `SkipHandlerMethods` request handling.

## [1.22.1] - 2021-10-25
### Changed

 * Fixes related to `SkipHandlerMethods` request handling.

## [1.22.0] - 2021-08-13
### Added
 * Add `SkipHandlerMethods` option as an allow-list of metohds that are handled by the override handler.

### Changed
 * Allow method registration if handler implements Register.
 * Internal changes related to relaying.

## [1.21.2] - 2021-05-19
### Changed

 * Internal changes related to relaying.

## [1.21.1] - 2021-03-17
### Changed
 * Change log level for connection create/close from info level to debug level to reduce noisy logs.

## [1.21.0] - 2020-12-13
### Changed
 * Internal changes related to relaying.

## [1.20.1] - 2020-09-24
### Fixed
 * Set ConnContext in the channel instead of the connection to avoid serialization
   errors since ConnectionOptions is sometimes embedded in configurations (#806)

## [1.20.0] - 2020-09-23
### Added
 * Support per-connection base context propagation for inbound/outbound connections (#801)

### Changed
 * Internal API changes related to relaying.

## [1.19.1] - 2020-08-03
### Fixed
 * Move OS-specific logic into OS-specific files to avoid compile issues on
   non-Unix platforms.

## [1.19.0] - 2020-05-21
### Fixed
 * Internal API changes related to relaying.

## [1.18.0] - 2020-03-30
### Added
 * Introspection now tracks last activity for reads and writes separately (#770)
 * Add options to allow overriding SendBufferSize per process name prefix (#772)

## [1.17.0] - 2020-02-18
### Added
 * Internal API changes related to relaying.

## [1.16.0] - 2019-10-14
### Added
 * Support custom Dialer for outbound connections (#759)

### Fixed
 * thrift: Handle TStruct serialization failures gracefully (#744)

## [1.15.0] - 2019-08-26
### Added
 * introspection: Introspect any channel by ID. (#756)

### Fixed
 * Ensure Introspection endpoints are always available. (#755)
 * Fix testutils.WithTestServer incorrectly using RelayHost when creating the server. (#750)

## [1.14.0] - 2019-05-20
### Added
 * Expose `CallOptions` caller name for transparent proxying (#741)

## [1.13.0] - 2019-04-04
### Added
 * Add `MaxCloseTime` which sets a timeout for graceful connection close. (#724)

### Changed
 * Optimize Thrift string field serialization by eliminating `[]byte(string)` allocation. (#729)

### Fixed
 * Return an error if transport header keys/values exceed the  maximum allowed string length. (#728)

## [1.12.0] - 2018-11-13
### Added
 * Add a channel, `ClosedCh`, to wait for a channel to close. (#718)
 * Add a Code of Conduct. (#711)

### Changed
 * Tweak error message when sending a large error to  mention that we're out of space. (#716)
 * Idle sweeper now skips connections that have pending calls. (#712)

## [1.11.0] - 2018-06-25
### Added
 * thrift: Support health check type in Health endpoint. (#696)

## [1.10.0] - 2018-04-02
### Added
 * Support blackholing requests to trigger client timeout without holding
   on to resources. (#681)
 * introspection: Include channel state in output. (#692)
 * introspection: Add inactive connections to output. (#686)

### Fixed
 * Inherit deadlines from parent context if available, and timeout is
   unspecified.
 * Ensure outbound tracing headers take precedence over application
   headers. (#683)

## [1.9.0] - 2018-01-31
### Added
 * stats: Add tally reporter to emit tagged metrics. (#676)
 * Add optional idle timeout, after which connections will be
   closed. (#681)

## [1.8.1] - 2017-11-21
### Fixed
 * Always log addresses as strings. (#669)

## [1.8.0] - 2017-11-06
### Added
 * Add opt-in active connection health checks. (#318)

### Changed
 * Improve error logging on `thrift.Server` errors. (#663)
 * Reduce memory usage for idle connections. (#658)
 * Unpin and reduce dependencies in `glide.yaml` by using `testImports`. (#649)

### Fixed
 * Don't close connections on ping errors.(#655)
 * Avoid holding on to closed connections' memory in peers. (#644)

## [1.7.0] - 2017-08-04
### Added
* Add `WithoutHeaders` to remove TChannel keys from a context.

### Changed
* Cancel the context on incoming calls if the client connection is closed.

## [1.6.0] - 2017-06-02
### Added
* Add `OnPeerStatusChanged` channel option to receive a notification each time
  the number of available connections changes for any given peer.

### Changed
* Locks Apache Thrift to version 0.9.3, 0.10.0 to maintain backward-compatibility.
* Set DiffServ (QoS) bit on outbound connections.

### Fixed
* Improve resilience of the frame parser.

## [1.5.0] - 2017-03-21
### Added
* Add `PeerList.Len` to expose the number of peers in the peer list.
* Add `PeerList.GetNew` to only return previously unselected peers.

## [1.4.0] - 2017-03-01
### Added
* Add version information to the channel's LocalPeerInfo.
* Add peers package for peer management utilities such as
  consistent peer selection.

### Fixed
* Fix SetScoreStrategy not rescoring existing peers. (#583).

## [1.3.0] - 2017-02-01
### Added
* Support Thrift namespaces for thrift-gen.
* Exposes the channel's RootPeerList with `channel.RootPeers()`.

## [1.2.3] - 2017-01-19
### Changed
* Improve error messages when an argument reader is closed without
  reading the EOF. (#567)

### Fixed
* thrift: Fix an issue where we return `nil` if we expected a Thrift exception
  but none was found (e.g., exception is from the future). (#566)
* Fix ListenIP selecting docker interfaces over physical networks. (#565)
* Fix for error when a Thrift payload has completed decoding and attempts
  to close the argument reader without waiting until EOF.  (#564)
* thrift-gen: Fix "namespace go" being ignored even though the Apache thrift
  generated code was respecting it. (#559)

## [1.2.2] - 2016-12-21
### Added
* Add a unique channel ID for introspection (#548)
* Expose local peer information on {Inbound,Outbound}Call (#537)
* Add remote peer info to connection logger and introspection (#514)

### Fixed
* Don't drop existing headers on a context when using Wrap(ctx) (#547)
* Setting response headers is not goroutine safe, allow using a child context
  for parallel sub-requests (#549).
* Fix context cancellation not cancelling Dial attempts (#541)
* Only select active connections for calls (#521)
* Treat hostPorts ending in ":0" in the init headers as ephemeral (#513)

## [1.2.1] - 2016-09-29
### Fixed
* Fix data race on headers when making concurrent calls using the same context. (#505)

## [1.2.0] - 2016-09-15
### Added
* Adds support for routing keys (the TChannel rk transport header).

## [1.1.0] - 2016-08-25
### Added
* Integrate OpenTracing for distributed tracing and context propagation.
  As long as a Zipkin-style tracing is configured, TChannel frames still
  send tracing information, and `CurrentSpan(ctx)` works as before.
  All tracer configuration must be handled through OpenTracing.
  (#426)

### Changed
* Improve error messages when using the json package and the host:port
  fails to connect. (#475)
* mockhyperbahn now using inbuilt TChannel relaying to implement in-process
  forwarding. (#472)
* Drop go1.4 support and add support for go1.7.
* Pass thrift.Context to the thrift.Server's response callback (#465)

## [1.0.9] - 2016-07-20
### Added
* Expose meta endpoints on the "tchannel" service name. (#459)
* Add Go version and tchannel-go library version to introspection. (#457)
* Expose the number of connections on a channel. (#451)

### Changed
* Better handling of peers where dialed host:port doesn't match the remote
  connection's reported host:port. (#452)

## [1.0.8] - 2016-07-15
### Fixed
* Remove dependency on "testing" from "tchannel-go" introduced in v1.0.7.

## [1.0.7] - 2016-07-15

### Added
* Add CallOptions() to IncomingCall which can be used as the call option
  when making outbound calls to proxy all transport headers.
* Add tracing information to all error frames generated by the library.
* Add GetHandlers for getting all registered methods on a subchannel.
* Expose the peer information for outbound calls.
* Support a separate connection timeout from the context timeout, useful for
  streaming calls where the stream timeout may be much longer than the
  connection timeout.

### Fixed
* Fix peer score not being calculated when adding a new outbound connections

## [1.0.6] - 2016-06-16
### Fixed
* Fix trace span encoding fields in the wrong order

## [1.0.5] - 2016-04-04
### Changed
* Use `context.Context` storage for headers so `thrift.Context` and
  `tchannel.ContextWithHeaders` can be passed to functions that use
  `context.Context`, and have them retain headers.
* `thrift.Server` allows a custom factory to be used for `thrift.Context`
  creation based on the underlying `context.Context` and headers map.
* Store goroutine stack traces on channel creation that can be accessed
  via introspection.

## [1.0.4] - 2016-03-09
### Added
* #228: Add registered methods to the introspection output.
* Add ability to set a global handler for a SubChannel.

### Fixed
* Improve handling of network failures during pending calls. Previously, calls
  would timeout, but now they fail as soon as the network failure is detected.
* Remove ephemeral peers with closed outbound connections.
* #233: Ensure errors returned from Thrift handlers have a non-nil value.

# 1.0.3 (2016-02-15)

### Added
* Introspection now includes information about all channels created
  in the current process.

### Changed
* Improved performance when writing Thrift structs
* Make closing message exchanges less disruptive, changes a panic due to
  closing a channel twice to an error log.

## [1.0.2] - 2016-01-29
### Changed
* Extend the `ContextBuilder` API to support setting the transport-level
  routing delegate header.
* Assorted logging and test improvements.

### Fixed
* Set a timeout when making new outbound connections to avoid hanging.
* Fix for #196: Make the initial Hyperbahn advertise more tolerant of transient
  timeouts.

## [1.0.1] - 2016-01-19
### Added
* Peers can now be removed using PeerList.Remove.
* Add ErrorHandlerFunc to create raw handlers that return errors.
* Retries try to avoid previously selected hosts, rather than just the
  host:port.
* Create an ArgReader interface (which is an alias for io.ReadCloser) for
  symmetry with ArgWriter.
* Add ArgReadable and ArgWritable interfaces for the common methods between
  calls and responses.
* Expose Thrift binary encoding methods (thrift.ReadStruct, thrift.WriteStruct,
  thrift.ReadHeaders, thrift.WriteHeaders) so callers can easily send Thrift
  payloads over the streaming interface.

### Fixed
* Bug fix for #181: Shuffle peers on PeerList.Add to avoid biases in peer
  selection.

## 1.0.0 - 2016-01-11
### Added
* First stable release.
* Support making calls with JSON, Thrift or raw payloads.
* Services use thrift-gen, and implement handlers with a `func(ctx, arg) (res,
  error)` signature.
* Support retries.
* Peer selection (peer heap, prefer incoming strategy, for use with Hyperbahn).
* Graceful channel shutdown.
* TCollector trace reporter with sampling support.
* Metrics collection with StatsD.
* Thrift support, including includes.

[//]: # (Version Links)
[1.34.4]: https://github.com/uber/tchannel-go/compare/v1.34.3...v1.34.4
[1.34.3]: https://github.com/uber/tchannel-go/compare/v1.34.2...v1.34.3
[1.34.2]: https://github.com/uber/tchannel-go/compare/v1.34.1...v1.34.2
[1.34.1]: https://github.com/uber/tchannel-go/compare/v1.34.0...v1.34.1
[1.34.0]: https://github.com/uber/tchannel-go/compare/v1.33.0...v1.34.0
[1.33.0]: https://github.com/uber/tchannel-go/compare/v1.32.1...v1.33.0
[1.32.1]: https://github.com/uber/tchannel-go/compare/v1.32.0...v1.32.1
[1.32.0]: https://github.com/uber/tchannel-go/compare/v1.31.0...v1.32.0
[1.31.0]: https://github.com/uber/tchannel-go/compare/v1.22.3...v1.31.0
[1.22.3]: https://github.com/uber/tchannel-go/compare/v1.22.2...v1.22.3
[1.22.1]: https://github.com/uber/tchannel-go/compare/v1.22.0...v1.22.1
[1.22.0]: https://github.com/uber/tchannel-go/compare/v1.21.2...v1.22.0
[1.21.2]: https://github.com/uber/tchannel-go/compare/v1.21.1...v1.21.2
[1.21.1]: https://github.com/uber/tchannel-go/compare/v1.21.0...v1.21.1
[1.21.0]: https://github.com/uber/tchannel-go/compare/v1.20.1...v1.21.0
[1.20.1]: https://github.com/uber/tchannel-go/compare/v1.20.0...v1.20.1
[1.20.0]: https://github.com/uber/tchannel-go/compare/v1.19.1...v1.20.0
[1.18.0]: https://github.com/uber/tchannel-go/compare/v1.17.0...v1.18.0
[1.17.0]: https://github.com/uber/tchannel-go/compare/v1.16.0...v1.17.0
[1.16.0]: https://github.com/uber/tchannel-go/compare/v1.15.0...v1.16.0
[1.15.0]: https://github.com/uber/tchannel-go/compare/v1.14.0...v1.15.0
[1.14.0]: https://github.com/uber/tchannel-go/compare/v1.13.0...v1.14.0
[1.13.0]: https://github.com/uber/tchannel-go/compare/v1.12.0...v1.13.0
[1.12.0]: https://github.com/uber/tchannel-go/compare/v1.11.0...v1.12.0
[1.11.0]: https://github.com/uber/tchannel-go/compare/v1.10.0...v1.11.0
[1.10.0]: https://github.com/uber/tchannel-go/compare/v1.9.0...v1.10.0
[1.9.0]: https://github.com/uber/tchannel-go/compare/v1.8.1...v1.9.0
[1.8.1]: https://github.com/uber/tchannel-go/compare/v1.8.0...v1.8.1
[1.8.0]: https://github.com/uber/tchannel-go/compare/v1.7.0...v1.8.0
[1.7.0]: https://github.com/uber/tchannel-go/compare/v1.6.0...v1.7.0
[1.6.0]: https://github.com/uber/tchannel-go/compare/v1.5.0...v1.6.0
[1.5.0]: https://github.com/uber/tchannel-go/compare/v1.4.0...v1.5.0
[1.4.0]: https://github.com/uber/tchannel-go/compare/v1.3.0...v1.4.0
[1.3.0]: https://github.com/uber/tchannel-go/compare/v1.2.3...v1.3.0
[1.2.3]: https://github.com/uber/tchannel-go/compare/v1.2.2...v1.2.3
[1.2.2]: https://github.com/uber/tchannel-go/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/uber/tchannel-go/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/uber/tchannel-go/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/uber/tchannel-go/compare/v1.0.9...v1.1.0
[1.0.9]: https://github.com/uber/tchannel-go/compare/v1.0.8...v1.0.9
[1.0.8]: https://github.com/uber/tchannel-go/compare/v1.0.7...v1.0.8
[1.0.7]: https://github.com/uber/tchannel-go/compare/v1.0.6...v1.0.7
[1.0.6]: https://github.com/uber/tchannel-go/compare/v1.0.5...v1.0.6
[1.0.5]: https://github.com/uber/tchannel-go/compare/v1.0.4...v1.0.5
[1.0.4]: https://github.com/uber/tchannel-go/compare/v1.0.2...v1.0.4
[1.0.2]: https://github.com/uber/tchannel-go/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/uber/tchannel-go/compare/v1.0.0...v1.0.1
