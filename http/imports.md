---
title: Imports
---

## Types

Type declarations included in the Imports module.

### Imports.**Resource**

```grain
record Resource<a> {
  handle: Int32,
  rep: a,
}
```

### Imports.**Error**

```grain
record Error {
  handle: Int32,
}
```

### Imports.**Pollable**

```grain
record Pollable {
  handle: Int32,
}
```

### Imports.**StreamError**

```grain
enum StreamError {
  LastOperationFailed(Error),
  Closed,
}
```

### Imports.**InputStream**

```grain
record InputStream {
  handle: Int32,
}
```

### Imports.**OutputStream**

```grain
record OutputStream {
  handle: Int32,
}
```

### Imports.**Instant**

```grain
type Instant = Uint64
```

### Imports.**Duration**

```grain
type Duration = Uint64
```

### Imports.**IoError**

```grain
type IoError = Error
```

### Imports.**Method**

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

### Imports.**Scheme**

```grain
enum Scheme {
  Http,
  Https,
  Other(String),
}
```

### Imports.**DnsErrorPayload**

```grain
record DnsErrorPayload {
  rcode: Option<String>,
  infoCode: Option<Uint16>,
}
```

### Imports.**TlsAlertReceivedPayload**

```grain
record TlsAlertReceivedPayload {
  alertId: Option<Uint8>,
  alertMessage: Option<String>,
}
```

### Imports.**FieldSizePayload**

```grain
record FieldSizePayload {
  fieldName: Option<String>,
  fieldSize: Option<Uint32>,
}
```

### Imports.**ErrorCode**

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

### Imports.**HeaderError**

```grain
enum HeaderError {
  InvalidSyntax,
  Forbidden,
  Immutable,
}
```

### Imports.**FieldKey**

```grain
type FieldKey = String
```

### Imports.**FieldValue**

```grain
type FieldValue = Bytes
```

### Imports.**Fields**

```grain
record Fields {
  handle: Int32,
}
```

### Imports.**Headers**

```grain
type Headers = Fields
```

### Imports.**Trailers**

```grain
type Trailers = Fields
```

### Imports.**IncomingRequest**

```grain
record IncomingRequest {
  handle: Int32,
}
```

### Imports.**OutgoingRequest**

```grain
record OutgoingRequest {
  handle: Int32,
}
```

### Imports.**RequestOptions**

```grain
record RequestOptions {
  handle: Int32,
}
```

### Imports.**ResponseOutparam**

```grain
record ResponseOutparam {
  handle: Int32,
}
```

### Imports.**StatusCode**

```grain
type StatusCode = Uint16
```

### Imports.**IncomingResponse**

```grain
record IncomingResponse {
  handle: Int32,
}
```

### Imports.**IncomingBody**

```grain
record IncomingBody {
  handle: Int32,
}
```

### Imports.**FutureTrailers**

```grain
record FutureTrailers {
  handle: Int32,
}
```

### Imports.**OutgoingResponse**

```grain
record OutgoingResponse {
  handle: Int32,
}
```

### Imports.**OutgoingBody**

```grain
record OutgoingBody {
  handle: Int32,
}
```

### Imports.**FutureIncomingResponse**

```grain
record FutureIncomingResponse {
  handle: Int32,
}
```

### Imports.**Datetime**

```grain
record Datetime {
  seconds: Uint64,
  nanoseconds: Uint32,
}
```

## Imports.Random

### Values

Functions and constants included in the Imports.Random module.

#### Imports.Random.**getRandomBytes**

```grain
getRandomBytes : Uint64 => Bytes
```

#### Imports.Random.**getRandomU64**

```grain
getRandomU64 : () => Uint64
```

## Imports.Error

### Imports.Error.Error

#### Values

Functions and constants included in the Imports.Error.Error module.

##### Imports.Error.Error.**toDebugString**

```grain
toDebugString : Error => String
```

## Imports.Poll

### Values

Functions and constants included in the Imports.Poll module.

#### Imports.Poll.**poll**

```grain
poll : List<Pollable> => List<Uint32>
```

### Imports.Poll.Pollable

#### Values

Functions and constants included in the Imports.Poll.Pollable module.

##### Imports.Poll.Pollable.**ready**

```grain
ready : Pollable => Bool
```

##### Imports.Poll.Pollable.**block**

```grain
block : Pollable => Void
```

## Imports.Streams

### Imports.Streams.InputStream

#### Values

Functions and constants included in the Imports.Streams.InputStream module.

##### Imports.Streams.InputStream.**read**

```grain
read : (InputStream, Uint64) => Result<Bytes, StreamError>
```

##### Imports.Streams.InputStream.**blockingRead**

```grain
blockingRead : (InputStream, Uint64) => Result<Bytes, StreamError>
```

##### Imports.Streams.InputStream.**skip**

```grain
skip : (InputStream, Uint64) => Result<Uint64, StreamError>
```

##### Imports.Streams.InputStream.**blockingSkip**

```grain
blockingSkip : (InputStream, Uint64) => Result<Uint64, StreamError>
```

##### Imports.Streams.InputStream.**subscribe**

```grain
subscribe : InputStream => Pollable
```

### Imports.Streams.OutputStream

#### Values

Functions and constants included in the Imports.Streams.OutputStream module.

##### Imports.Streams.OutputStream.**checkWrite**

```grain
checkWrite : OutputStream => Result<Uint64, StreamError>
```

##### Imports.Streams.OutputStream.**write**

```grain
write : (OutputStream, Bytes) => Result<Void, StreamError>
```

##### Imports.Streams.OutputStream.**blockingWriteAndFlush**

```grain
blockingWriteAndFlush : (OutputStream, Bytes) => Result<Void, StreamError>
```

##### Imports.Streams.OutputStream.**flush**

```grain
flush : OutputStream => Result<Void, StreamError>
```

##### Imports.Streams.OutputStream.**blockingFlush**

```grain
blockingFlush : OutputStream => Result<Void, StreamError>
```

##### Imports.Streams.OutputStream.**subscribe**

```grain
subscribe : OutputStream => Pollable
```

##### Imports.Streams.OutputStream.**writeZeroes**

```grain
writeZeroes : (OutputStream, Uint64) => Result<Void, StreamError>
```

##### Imports.Streams.OutputStream.**blockingWriteZeroesAndFlush**

```grain
blockingWriteZeroesAndFlush :
  (OutputStream, Uint64) => Result<Void, StreamError>
```

##### Imports.Streams.OutputStream.**splice**

```grain
splice : (OutputStream, InputStream, Uint64) => Result<Uint64, StreamError>
```

##### Imports.Streams.OutputStream.**blockingSplice**

```grain
blockingSplice :
  (OutputStream, InputStream, Uint64) => Result<Uint64, StreamError>
```

## Imports.Stdout

### Values

Functions and constants included in the Imports.Stdout module.

#### Imports.Stdout.**getStdout**

```grain
getStdout : () => OutputStream
```

## Imports.Stderr

### Values

Functions and constants included in the Imports.Stderr module.

#### Imports.Stderr.**getStderr**

```grain
getStderr : () => OutputStream
```

## Imports.Stdin

### Values

Functions and constants included in the Imports.Stdin module.

#### Imports.Stdin.**getStdin**

```grain
getStdin : () => InputStream
```

## Imports.MonotonicClock

### Values

Functions and constants included in the Imports.MonotonicClock module.

#### Imports.MonotonicClock.**now**

```grain
now : () => Instant
```

#### Imports.MonotonicClock.**resolution**

```grain
resolution : () => Duration
```

#### Imports.MonotonicClock.**subscribeInstant**

```grain
subscribeInstant : Instant => Pollable
```

#### Imports.MonotonicClock.**subscribeDuration**

```grain
subscribeDuration : Duration => Pollable
```

## Imports.Types

### Values

Functions and constants included in the Imports.Types module.

#### Imports.Types.**httpErrorCode**

```grain
httpErrorCode : IoError => Option<ErrorCode>
```

### Imports.Types.Fields

#### Values

Functions and constants included in the Imports.Types.Fields module.

##### Imports.Types.Fields.**constructor**

```grain
constructor : () => Fields
```

##### Imports.Types.Fields.**fromList**

```grain
fromList : List<(FieldKey, FieldValue)> => Result<Fields, HeaderError>
```

##### Imports.Types.Fields.**get**

```grain
get : (Fields, FieldKey) => List<FieldValue>
```

##### Imports.Types.Fields.**has**

```grain
has : (Fields, FieldKey) => Bool
```

##### Imports.Types.Fields.**set**

```grain
set : (Fields, FieldKey, List<FieldValue>) => Result<Void, HeaderError>
```

##### Imports.Types.Fields.**delete**

```grain
delete : (Fields, FieldKey) => Result<Void, HeaderError>
```

##### Imports.Types.Fields.**append**

```grain
append : (Fields, FieldKey, FieldValue) => Result<Void, HeaderError>
```

##### Imports.Types.Fields.**entries**

```grain
entries : Fields => List<(FieldKey, FieldValue)>
```

##### Imports.Types.Fields.**clone**

```grain
clone : Fields => Fields
```

### Imports.Types.IncomingRequest

#### Values

Functions and constants included in the Imports.Types.IncomingRequest module.

##### Imports.Types.IncomingRequest.**method**

```grain
method : IncomingRequest => Method
```

##### Imports.Types.IncomingRequest.**pathWithQuery**

```grain
pathWithQuery : IncomingRequest => Option<String>
```

##### Imports.Types.IncomingRequest.**scheme**

```grain
scheme : IncomingRequest => Option<Scheme>
```

##### Imports.Types.IncomingRequest.**authority**

```grain
authority : IncomingRequest => Option<String>
```

##### Imports.Types.IncomingRequest.**headers**

```grain
headers : IncomingRequest => Headers
```

##### Imports.Types.IncomingRequest.**consume**

```grain
consume : IncomingRequest => Result<IncomingBody, Void>
```

### Imports.Types.OutgoingRequest

#### Values

Functions and constants included in the Imports.Types.OutgoingRequest module.

##### Imports.Types.OutgoingRequest.**constructor**

```grain
constructor : Headers => OutgoingRequest
```

##### Imports.Types.OutgoingRequest.**body**

```grain
body : OutgoingRequest => Result<OutgoingBody, Void>
```

##### Imports.Types.OutgoingRequest.**method**

```grain
method : OutgoingRequest => Method
```

##### Imports.Types.OutgoingRequest.**setMethod**

```grain
setMethod : (OutgoingRequest, Method) => Result<Void, Void>
```

##### Imports.Types.OutgoingRequest.**pathWithQuery**

```grain
pathWithQuery : OutgoingRequest => Option<String>
```

##### Imports.Types.OutgoingRequest.**setPathWithQuery**

```grain
setPathWithQuery : (OutgoingRequest, Option<String>) => Result<Void, Void>
```

##### Imports.Types.OutgoingRequest.**scheme**

```grain
scheme : OutgoingRequest => Option<Scheme>
```

##### Imports.Types.OutgoingRequest.**setScheme**

```grain
setScheme : (OutgoingRequest, Option<Scheme>) => Result<Void, Void>
```

##### Imports.Types.OutgoingRequest.**authority**

```grain
authority : OutgoingRequest => Option<String>
```

##### Imports.Types.OutgoingRequest.**setAuthority**

```grain
setAuthority : (OutgoingRequest, Option<String>) => Result<Void, Void>
```

##### Imports.Types.OutgoingRequest.**headers**

```grain
headers : OutgoingRequest => Headers
```

### Imports.Types.RequestOptions

#### Values

Functions and constants included in the Imports.Types.RequestOptions module.

##### Imports.Types.RequestOptions.**constructor**

```grain
constructor : () => RequestOptions
```

##### Imports.Types.RequestOptions.**connectTimeout**

```grain
connectTimeout : RequestOptions => Option<Duration>
```

##### Imports.Types.RequestOptions.**setConnectTimeout**

```grain
setConnectTimeout : (RequestOptions, Option<Duration>) => Result<Void, Void>
```

##### Imports.Types.RequestOptions.**firstByteTimeout**

```grain
firstByteTimeout : RequestOptions => Option<Duration>
```

##### Imports.Types.RequestOptions.**setFirstByteTimeout**

```grain
setFirstByteTimeout :
  (RequestOptions, Option<Duration>) => Result<Void, Void>
```

##### Imports.Types.RequestOptions.**betweenBytesTimeout**

```grain
betweenBytesTimeout : RequestOptions => Option<Duration>
```

##### Imports.Types.RequestOptions.**setBetweenBytesTimeout**

```grain
setBetweenBytesTimeout :
  (RequestOptions, Option<Duration>) => Result<Void, Void>
```

### Imports.Types.ResponseOutparam

#### Values

Functions and constants included in the Imports.Types.ResponseOutparam module.

##### Imports.Types.ResponseOutparam.**set**

```grain
set : (ResponseOutparam, Result<OutgoingResponse, ErrorCode>) => Void
```

### Imports.Types.IncomingResponse

#### Values

Functions and constants included in the Imports.Types.IncomingResponse module.

##### Imports.Types.IncomingResponse.**status**

```grain
status : IncomingResponse => StatusCode
```

##### Imports.Types.IncomingResponse.**headers**

```grain
headers : IncomingResponse => Headers
```

##### Imports.Types.IncomingResponse.**consume**

```grain
consume : IncomingResponse => Result<IncomingBody, Void>
```

### Imports.Types.IncomingBody

#### Values

Functions and constants included in the Imports.Types.IncomingBody module.

##### Imports.Types.IncomingBody.**stream**

```grain
stream : IncomingBody => Result<InputStream, Void>
```

##### Imports.Types.IncomingBody.**finish**

```grain
finish : IncomingBody => FutureTrailers
```

### Imports.Types.FutureTrailers

#### Values

Functions and constants included in the Imports.Types.FutureTrailers module.

##### Imports.Types.FutureTrailers.**subscribe**

```grain
subscribe : FutureTrailers => Pollable
```

##### Imports.Types.FutureTrailers.**get**

```grain
get :
  FutureTrailers => Option<Result<Result<Option<Trailers>, ErrorCode>, Void>>
```

### Imports.Types.OutgoingResponse

#### Values

Functions and constants included in the Imports.Types.OutgoingResponse module.

##### Imports.Types.OutgoingResponse.**constructor**

```grain
constructor : Headers => OutgoingResponse
```

##### Imports.Types.OutgoingResponse.**statusCode**

```grain
statusCode : OutgoingResponse => StatusCode
```

##### Imports.Types.OutgoingResponse.**setStatusCode**

```grain
setStatusCode : (OutgoingResponse, StatusCode) => Result<Void, Void>
```

##### Imports.Types.OutgoingResponse.**headers**

```grain
headers : OutgoingResponse => Headers
```

##### Imports.Types.OutgoingResponse.**body**

```grain
body : OutgoingResponse => Result<OutgoingBody, Void>
```

### Imports.Types.OutgoingBody

#### Values

Functions and constants included in the Imports.Types.OutgoingBody module.

##### Imports.Types.OutgoingBody.**write**

```grain
write : OutgoingBody => Result<OutputStream, Void>
```

##### Imports.Types.OutgoingBody.**finish**

```grain
finish : (OutgoingBody, Option<Trailers>) => Result<Void, ErrorCode>
```

### Imports.Types.FutureIncomingResponse

#### Values

Functions and constants included in the Imports.Types.FutureIncomingResponse module.

##### Imports.Types.FutureIncomingResponse.**subscribe**

```grain
subscribe : FutureIncomingResponse => Pollable
```

##### Imports.Types.FutureIncomingResponse.**get**

```grain
get :
  FutureIncomingResponse =>
   Option<Result<Result<IncomingResponse, ErrorCode>, Void>>
```

## Imports.OutgoingHandler

### Values

Functions and constants included in the Imports.OutgoingHandler module.

#### Imports.OutgoingHandler.**handle**

```grain
handle :
  (OutgoingRequest, Option<RequestOptions>) =>
   Result<FutureIncomingResponse, ErrorCode>
```

## Imports.WallClock

### Values

Functions and constants included in the Imports.WallClock module.

#### Imports.WallClock.**now**

```grain
now : () => Datetime
```

#### Imports.WallClock.**resolution**

```grain
resolution : () => Datetime
```

