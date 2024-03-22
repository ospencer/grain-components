---
title: Proxy
---

## Types

Type declarations included in the Proxy module.

### Proxy.**Resource**

```grain
record Resource<a> {
  handle: Int32,
  rep: a,
}
```

### Proxy.**Pollable**

```grain
record Pollable {
  handle: Int32,
}
```

### Proxy.**Instant**

```grain
type Instant = Uint64
```

### Proxy.**Duration**

```grain
type Duration = Uint64
```

### Proxy.**Error**

```grain
record Error {
  handle: Int32,
}
```

### Proxy.**StreamError**

```grain
enum StreamError {
  LastOperationFailed(Error),
  Closed,
}
```

### Proxy.**InputStream**

```grain
record InputStream {
  handle: Int32,
}
```

### Proxy.**OutputStream**

```grain
record OutputStream {
  handle: Int32,
}
```

### Proxy.**IoError**

```grain
type IoError = Error
```

### Proxy.**Method**

```grain
enum Method {
  Get,
  Head,
  Post,
  Put,
  Delete,
  Connect,
  Options,
  Trace,
  Patch,
  Other(String),
}
```

### Proxy.**Scheme**

```grain
enum Scheme {
  Http,
  Https,
  Other(String),
}
```

### Proxy.**DnsErrorPayload**

```grain
record DnsErrorPayload {
  rcode: Option<String>,
  infoCode: Option<Uint16>,
}
```

### Proxy.**TlsAlertReceivedPayload**

```grain
record TlsAlertReceivedPayload {
  alertId: Option<Uint8>,
  alertMessage: Option<String>,
}
```

### Proxy.**FieldSizePayload**

```grain
record FieldSizePayload {
  fieldName: Option<String>,
  fieldSize: Option<Uint32>,
}
```

### Proxy.**ErrorCode**

```grain
enum ErrorCode {
  DnsTimeout,
  DnsError(DnsErrorPayload),
  DestinationNotFound,
  DestinationUnavailable,
  DestinationIpProhibited,
  DestinationIpUnroutable,
  ConnectionRefused,
  ConnectionTerminated,
  ConnectionTimeout,
  ConnectionReadTimeout,
  ConnectionWriteTimeout,
  ConnectionLimitReached,
  TlsProtocolError,
  TlsCertificateError,
  TlsAlertReceived(TlsAlertReceivedPayload),
  HttpRequestDenied,
  HttpRequestLengthRequired,
  HttpRequestBodySize(Option<Uint64>),
  HttpRequestMethodInvalid,
  HttpRequestUriInvalid,
  HttpRequestUriTooLong,
  HttpRequestHeaderSectionSize(Option<Uint32>),
  HttpRequestHeaderSize(Option<FieldSizePayload>),
  HttpRequestTrailerSectionSize(Option<Uint32>),
  HttpRequestTrailerSize(FieldSizePayload),
  HttpResponseIncomplete,
  HttpResponseHeaderSectionSize(Option<Uint32>),
  HttpResponseHeaderSize(FieldSizePayload),
  HttpResponseBodySize(Option<Uint64>),
  HttpResponseTrailerSectionSize(Option<Uint32>),
  HttpResponseTrailerSize(FieldSizePayload),
  HttpResponseTransferCoding(Option<String>),
  HttpResponseContentCoding(Option<String>),
  HttpResponseTimeout,
  HttpUpgradeFailed,
  HttpProtocolError,
  LoopDetected,
  ConfigurationError,
  InternalError(Option<String>),
}
```

### Proxy.**HeaderError**

```grain
enum HeaderError {
  InvalidSyntax,
  Forbidden,
  Immutable,
}
```

### Proxy.**FieldKey**

```grain
type FieldKey = String
```

### Proxy.**FieldValue**

```grain
type FieldValue = Bytes
```

### Proxy.**Fields**

```grain
record Fields {
  handle: Int32,
}
```

### Proxy.**Headers**

```grain
type Headers = Fields
```

### Proxy.**Trailers**

```grain
type Trailers = Fields
```

### Proxy.**IncomingRequest**

```grain
record IncomingRequest {
  handle: Int32,
}
```

### Proxy.**OutgoingRequest**

```grain
record OutgoingRequest {
  handle: Int32,
}
```

### Proxy.**RequestOptions**

```grain
record RequestOptions {
  handle: Int32,
}
```

### Proxy.**ResponseOutparam**

```grain
record ResponseOutparam {
  handle: Int32,
}
```

### Proxy.**StatusCode**

```grain
type StatusCode = Uint16
```

### Proxy.**IncomingResponse**

```grain
record IncomingResponse {
  handle: Int32,
}
```

### Proxy.**IncomingBody**

```grain
record IncomingBody {
  handle: Int32,
}
```

### Proxy.**FutureTrailers**

```grain
record FutureTrailers {
  handle: Int32,
}
```

### Proxy.**OutgoingResponse**

```grain
record OutgoingResponse {
  handle: Int32,
}
```

### Proxy.**OutgoingBody**

```grain
record OutgoingBody {
  handle: Int32,
}
```

### Proxy.**FutureIncomingResponse**

```grain
record FutureIncomingResponse {
  handle: Int32,
}
```

### Proxy.**Datetime**

```grain
record Datetime {
  seconds: Uint64,
  nanoseconds: Uint32,
}
```

## Proxy.Poll

### Values

Functions and constants included in the Proxy.Poll module.

#### Proxy.Poll.**poll**

```grain
poll : List<Pollable> => List<Uint32>
```

### Proxy.Poll.Pollable

#### Values

Functions and constants included in the Proxy.Poll.Pollable module.

##### Proxy.Poll.Pollable.**ready**

```grain
ready : Pollable => Bool
```

##### Proxy.Poll.Pollable.**block**

```grain
block : Pollable => Void
```

## Proxy.MonotonicClock

### Values

Functions and constants included in the Proxy.MonotonicClock module.

#### Proxy.MonotonicClock.**now**

```grain
now : () => Instant
```

#### Proxy.MonotonicClock.**resolution**

```grain
resolution : () => Duration
```

#### Proxy.MonotonicClock.**subscribeInstant**

```grain
subscribeInstant : Instant => Pollable
```

#### Proxy.MonotonicClock.**subscribeDuration**

```grain
subscribeDuration : Duration => Pollable
```

## Proxy.Error

### Proxy.Error.Error

#### Values

Functions and constants included in the Proxy.Error.Error module.

##### Proxy.Error.Error.**toDebugString**

```grain
toDebugString : Error => String
```

## Proxy.Streams

### Proxy.Streams.InputStream

#### Values

Functions and constants included in the Proxy.Streams.InputStream module.

##### Proxy.Streams.InputStream.**read**

```grain
read : (InputStream, Uint64) => Result<Bytes, StreamError>
```

##### Proxy.Streams.InputStream.**blockingRead**

```grain
blockingRead : (InputStream, Uint64) => Result<Bytes, StreamError>
```

##### Proxy.Streams.InputStream.**skip**

```grain
skip : (InputStream, Uint64) => Result<Uint64, StreamError>
```

##### Proxy.Streams.InputStream.**blockingSkip**

```grain
blockingSkip : (InputStream, Uint64) => Result<Uint64, StreamError>
```

##### Proxy.Streams.InputStream.**subscribe**

```grain
subscribe : InputStream => Pollable
```

### Proxy.Streams.OutputStream

#### Values

Functions and constants included in the Proxy.Streams.OutputStream module.

##### Proxy.Streams.OutputStream.**checkWrite**

```grain
checkWrite : OutputStream => Result<Uint64, StreamError>
```

##### Proxy.Streams.OutputStream.**write**

```grain
write : (OutputStream, Bytes) => Result<Void, StreamError>
```

##### Proxy.Streams.OutputStream.**blockingWriteAndFlush**

```grain
blockingWriteAndFlush : (OutputStream, Bytes) => Result<Void, StreamError>
```

##### Proxy.Streams.OutputStream.**flush**

```grain
flush : OutputStream => Result<Void, StreamError>
```

##### Proxy.Streams.OutputStream.**blockingFlush**

```grain
blockingFlush : OutputStream => Result<Void, StreamError>
```

##### Proxy.Streams.OutputStream.**subscribe**

```grain
subscribe : OutputStream => Pollable
```

##### Proxy.Streams.OutputStream.**writeZeroes**

```grain
writeZeroes : (OutputStream, Uint64) => Result<Void, StreamError>
```

##### Proxy.Streams.OutputStream.**blockingWriteZeroesAndFlush**

```grain
blockingWriteZeroesAndFlush :
  (OutputStream, Uint64) => Result<Void, StreamError>
```

##### Proxy.Streams.OutputStream.**splice**

```grain
splice : (OutputStream, InputStream, Uint64) => Result<Uint64, StreamError>
```

##### Proxy.Streams.OutputStream.**blockingSplice**

```grain
blockingSplice :
  (OutputStream, InputStream, Uint64) => Result<Uint64, StreamError>
```

## Proxy.Types

### Values

Functions and constants included in the Proxy.Types module.

#### Proxy.Types.**httpErrorCode**

```grain
httpErrorCode : IoError => Option<ErrorCode>
```

### Proxy.Types.Fields

#### Values

Functions and constants included in the Proxy.Types.Fields module.

##### Proxy.Types.Fields.**constructor**

```grain
constructor : () => Fields
```

##### Proxy.Types.Fields.**fromList**

```grain
fromList : List<(FieldKey, FieldValue)> => Result<Fields, HeaderError>
```

##### Proxy.Types.Fields.**get**

```grain
get : (Fields, FieldKey) => List<FieldValue>
```

##### Proxy.Types.Fields.**has**

```grain
has : (Fields, FieldKey) => Bool
```

##### Proxy.Types.Fields.**set**

```grain
set : (Fields, FieldKey, List<FieldValue>) => Result<Void, HeaderError>
```

##### Proxy.Types.Fields.**delete**

```grain
delete : (Fields, FieldKey) => Result<Void, HeaderError>
```

##### Proxy.Types.Fields.**append**

```grain
append : (Fields, FieldKey, FieldValue) => Result<Void, HeaderError>
```

##### Proxy.Types.Fields.**entries**

```grain
entries : Fields => List<(FieldKey, FieldValue)>
```

##### Proxy.Types.Fields.**clone**

```grain
clone : Fields => Fields
```

### Proxy.Types.IncomingRequest

#### Values

Functions and constants included in the Proxy.Types.IncomingRequest module.

##### Proxy.Types.IncomingRequest.**method**

```grain
method : IncomingRequest => Method
```

##### Proxy.Types.IncomingRequest.**pathWithQuery**

```grain
pathWithQuery : IncomingRequest => Option<String>
```

##### Proxy.Types.IncomingRequest.**scheme**

```grain
scheme : IncomingRequest => Option<Scheme>
```

##### Proxy.Types.IncomingRequest.**authority**

```grain
authority : IncomingRequest => Option<String>
```

##### Proxy.Types.IncomingRequest.**headers**

```grain
headers : IncomingRequest => Headers
```

##### Proxy.Types.IncomingRequest.**consume**

```grain
consume : IncomingRequest => Result<IncomingBody, Void>
```

### Proxy.Types.OutgoingRequest

#### Values

Functions and constants included in the Proxy.Types.OutgoingRequest module.

##### Proxy.Types.OutgoingRequest.**constructor**

```grain
constructor : Headers => OutgoingRequest
```

##### Proxy.Types.OutgoingRequest.**body**

```grain
body : OutgoingRequest => Result<OutgoingBody, Void>
```

##### Proxy.Types.OutgoingRequest.**method**

```grain
method : OutgoingRequest => Method
```

##### Proxy.Types.OutgoingRequest.**setMethod**

```grain
setMethod : (OutgoingRequest, Method) => Result<Void, Void>
```

##### Proxy.Types.OutgoingRequest.**pathWithQuery**

```grain
pathWithQuery : OutgoingRequest => Option<String>
```

##### Proxy.Types.OutgoingRequest.**setPathWithQuery**

```grain
setPathWithQuery : (OutgoingRequest, Option<String>) => Result<Void, Void>
```

##### Proxy.Types.OutgoingRequest.**scheme**

```grain
scheme : OutgoingRequest => Option<Scheme>
```

##### Proxy.Types.OutgoingRequest.**setScheme**

```grain
setScheme : (OutgoingRequest, Option<Scheme>) => Result<Void, Void>
```

##### Proxy.Types.OutgoingRequest.**authority**

```grain
authority : OutgoingRequest => Option<String>
```

##### Proxy.Types.OutgoingRequest.**setAuthority**

```grain
setAuthority : (OutgoingRequest, Option<String>) => Result<Void, Void>
```

##### Proxy.Types.OutgoingRequest.**headers**

```grain
headers : OutgoingRequest => Headers
```

### Proxy.Types.RequestOptions

#### Values

Functions and constants included in the Proxy.Types.RequestOptions module.

##### Proxy.Types.RequestOptions.**constructor**

```grain
constructor : () => RequestOptions
```

##### Proxy.Types.RequestOptions.**connectTimeout**

```grain
connectTimeout : RequestOptions => Option<Duration>
```

##### Proxy.Types.RequestOptions.**setConnectTimeout**

```grain
setConnectTimeout : (RequestOptions, Option<Duration>) => Result<Void, Void>
```

##### Proxy.Types.RequestOptions.**firstByteTimeout**

```grain
firstByteTimeout : RequestOptions => Option<Duration>
```

##### Proxy.Types.RequestOptions.**setFirstByteTimeout**

```grain
setFirstByteTimeout :
  (RequestOptions, Option<Duration>) => Result<Void, Void>
```

##### Proxy.Types.RequestOptions.**betweenBytesTimeout**

```grain
betweenBytesTimeout : RequestOptions => Option<Duration>
```

##### Proxy.Types.RequestOptions.**setBetweenBytesTimeout**

```grain
setBetweenBytesTimeout :
  (RequestOptions, Option<Duration>) => Result<Void, Void>
```

### Proxy.Types.ResponseOutparam

#### Values

Functions and constants included in the Proxy.Types.ResponseOutparam module.

##### Proxy.Types.ResponseOutparam.**set**

```grain
set : (ResponseOutparam, Result<OutgoingResponse, ErrorCode>) => Void
```

### Proxy.Types.IncomingResponse

#### Values

Functions and constants included in the Proxy.Types.IncomingResponse module.

##### Proxy.Types.IncomingResponse.**status**

```grain
status : IncomingResponse => StatusCode
```

##### Proxy.Types.IncomingResponse.**headers**

```grain
headers : IncomingResponse => Headers
```

##### Proxy.Types.IncomingResponse.**consume**

```grain
consume : IncomingResponse => Result<IncomingBody, Void>
```

### Proxy.Types.IncomingBody

#### Values

Functions and constants included in the Proxy.Types.IncomingBody module.

##### Proxy.Types.IncomingBody.**stream**

```grain
stream : IncomingBody => Result<InputStream, Void>
```

##### Proxy.Types.IncomingBody.**finish**

```grain
finish : IncomingBody => FutureTrailers
```

### Proxy.Types.FutureTrailers

#### Values

Functions and constants included in the Proxy.Types.FutureTrailers module.

##### Proxy.Types.FutureTrailers.**subscribe**

```grain
subscribe : FutureTrailers => Pollable
```

##### Proxy.Types.FutureTrailers.**get**

```grain
get :
  FutureTrailers => Option<Result<Result<Option<Trailers>, ErrorCode>, Void>>
```

### Proxy.Types.OutgoingResponse

#### Values

Functions and constants included in the Proxy.Types.OutgoingResponse module.

##### Proxy.Types.OutgoingResponse.**constructor**

```grain
constructor : Headers => OutgoingResponse
```

##### Proxy.Types.OutgoingResponse.**statusCode**

```grain
statusCode : OutgoingResponse => StatusCode
```

##### Proxy.Types.OutgoingResponse.**setStatusCode**

```grain
setStatusCode : (OutgoingResponse, StatusCode) => Result<Void, Void>
```

##### Proxy.Types.OutgoingResponse.**headers**

```grain
headers : OutgoingResponse => Headers
```

##### Proxy.Types.OutgoingResponse.**body**

```grain
body : OutgoingResponse => Result<OutgoingBody, Void>
```

### Proxy.Types.OutgoingBody

#### Values

Functions and constants included in the Proxy.Types.OutgoingBody module.

##### Proxy.Types.OutgoingBody.**write**

```grain
write : OutgoingBody => Result<OutputStream, Void>
```

##### Proxy.Types.OutgoingBody.**finish**

```grain
finish : (OutgoingBody, Option<Trailers>) => Result<Void, ErrorCode>
```

### Proxy.Types.FutureIncomingResponse

#### Values

Functions and constants included in the Proxy.Types.FutureIncomingResponse module.

##### Proxy.Types.FutureIncomingResponse.**subscribe**

```grain
subscribe : FutureIncomingResponse => Pollable
```

##### Proxy.Types.FutureIncomingResponse.**get**

```grain
get :
  FutureIncomingResponse =>
   Option<Result<Result<IncomingResponse, ErrorCode>, Void>>
```

## Proxy.Random

### Values

Functions and constants included in the Proxy.Random module.

#### Proxy.Random.**getRandomBytes**

```grain
getRandomBytes : Uint64 => Bytes
```

#### Proxy.Random.**getRandomU64**

```grain
getRandomU64 : () => Uint64
```

## Proxy.Stdout

### Values

Functions and constants included in the Proxy.Stdout module.

#### Proxy.Stdout.**getStdout**

```grain
getStdout : () => OutputStream
```

## Proxy.Stderr

### Values

Functions and constants included in the Proxy.Stderr module.

#### Proxy.Stderr.**getStderr**

```grain
getStderr : () => OutputStream
```

## Proxy.Stdin

### Values

Functions and constants included in the Proxy.Stdin module.

#### Proxy.Stdin.**getStdin**

```grain
getStdin : () => InputStream
```

## Proxy.OutgoingHandler

### Values

Functions and constants included in the Proxy.OutgoingHandler module.

#### Proxy.OutgoingHandler.**handle**

```grain
handle :
  (OutgoingRequest, Option<RequestOptions>) =>
   Result<FutureIncomingResponse, ErrorCode>
```

## Proxy.WallClock

### Values

Functions and constants included in the Proxy.WallClock module.

#### Proxy.WallClock.**now**

```grain
now : () => Datetime
```

#### Proxy.WallClock.**resolution**

```grain
resolution : () => Datetime
```

