[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `webworker.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/lib/webworker.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LibDefinition` | `../variable` |
| `TYPE` | `./base-config` |
| `TYPE_VALUE` | `./base-config` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `webworker` | `LibDefinition` | const | `{
  libs: [],
  variables: [
    ['AddEventListenerOptions', TYPE],
    ['AesCbcParams', TYPE],
    ['AesCtrParams', TYPE],
    ['AesDerivedKeyParams', TYPE],
    ['AesGcmParams', TYPE],
    ['AesKeyAlgorithm', TYPE],
    ['AesKeyGenParams', TYPE],
    ['Algorithm', TYPE],
    ['AudioConfiguration', TYPE],
    ['AudioDataCopyToOptions', TYPE],
    ['AudioDataInit', TYPE],
    ['AudioDecoderConfig', TYPE],
    ['AudioDecoderInit', TYPE],
    ['AudioDecoderSupport', TYPE],
    ['AudioEncoderConfig', TYPE],
    ['AudioEncoderInit', TYPE],
    ['AudioEncoderSupport', TYPE],
    ['AvcEncoderConfig', TYPE],
    ['BlobPropertyBag', TYPE],
    ['CSSMatrixComponentOptions', TYPE],
    ['CSSNumericType', TYPE],
    ['CacheQueryOptions', TYPE],
    ['ClientQueryOptions', TYPE],
    ['CloseEventInit', TYPE],
    ['CryptoKeyPair', TYPE],
    ['CustomEventInit', TYPE],
    ['DOMMatrix2DInit', TYPE],
    ['DOMMatrixInit', TYPE],
    ['DOMPointInit', TYPE],
    ['DOMQuadInit', TYPE],
    ['DOMRectInit', TYPE],
    ['EcKeyGenParams', TYPE],
    ['EcKeyImportParams', TYPE],
    ['EcdhKeyDeriveParams', TYPE],
    ['EcdsaParams', TYPE],
    ['EncodedAudioChunkInit', TYPE],
    ['EncodedAudioChunkMetadata', TYPE],
    ['EncodedVideoChunkInit', TYPE],
    ['EncodedVideoChunkMetadata', TYPE],
    ['ErrorEventInit', TYPE],
    ['EventInit', TYPE],
    ['EventListenerOptions', TYPE],
    ['EventSourceInit', TYPE],
    ['ExtendableEventInit', TYPE],
    ['ExtendableMessageEventInit', TYPE],
    ['FetchEventInit', TYPE],
    ['FilePropertyBag', TYPE],
    ['FileSystemCreateWritableOptions', TYPE],
    ['FileSystemGetDirectoryOptions', TYPE],
    ['FileSystemGetFileOptions', TYPE],
    ['FileSystemReadWriteOptions', TYPE],
    ['FileSystemRemoveOptions', TYPE],
    ['FontFaceDescriptors', TYPE],
    ['FontFaceSetLoadEventInit', TYPE],
    ['GetNotificationOptions', TYPE],
    ['HkdfParams', TYPE],
    ['HmacImportParams', TYPE],
    ['HmacKeyGenParams', TYPE],
    ['IDBDatabaseInfo', TYPE],
    ['IDBIndexParameters', TYPE],
    ['IDBObjectStoreParameters', TYPE],
    ['IDBTransactionOptions', TYPE],
    ['IDBVersionChangeEventInit', TYPE],
    ['ImageBitmapOptions', TYPE],
    ['ImageBitmapRenderingContextSettings', TYPE],
    ['ImageDataSettings', TYPE],
    ['ImageDecodeOptions', TYPE],
    ['ImageDecodeResult', TYPE],
    ['ImageDecoderInit', TYPE],
    ['ImageEncodeOptions', TYPE],
    ['JsonWebKey', TYPE],
    ['KeyAlgorithm', TYPE],
    ['LockInfo', TYPE],
    ['LockManagerSnapshot', TYPE],
    ['LockOptions', TYPE],
    ['MediaCapabilitiesDecodingInfo', TYPE],
    ['MediaCapabilitiesEncodingInfo', TYPE],
    ['MediaCapabilitiesInfo', TYPE],
    ['MediaConfiguration', TYPE],
    ['MediaDecodingConfiguration', TYPE],
    ['MediaEncodingConfiguration', TYPE],
    ['MediaStreamTrackProcessorInit', TYPE],
    ['MessageEventInit', TYPE],
    ['MultiCacheQueryOptions', TYPE],
    ['NavigationPreloadState', TYPE],
    ['NotificationEventInit', TYPE],
    ['NotificationOptions', TYPE],
    ['OpusEncoderConfig', TYPE],
    ['Pbkdf2Params', TYPE],
    ['PerformanceMarkOptions', TYPE],
    ['PerformanceMeasureOptions', TYPE],
    ['PerformanceObserverInit', TYPE],
    ['PermissionDescriptor', TYPE],
    ['PlaneLayout', TYPE],
    ['ProgressEventInit', TYPE],
    ['PromiseRejectionEventInit', TYPE],
    ['PushEventInit', TYPE],
    ['PushSubscriptionJSON', TYPE],
    ['PushSubscriptionOptionsInit', TYPE],
    ['QueuingStrategy', TYPE],
    ['QueuingStrategyInit', TYPE],
    ['RTCEncodedAudioFrameMetadata', TYPE],
    ['RTCEncodedVideoFrameMetadata', TYPE],
    ['ReadableStreamGetReaderOptions', TYPE],
    ['ReadableStreamIteratorOptions', TYPE],
    ['ReadableStreamReadDoneResult', TYPE],
    ['ReadableStreamReadValueResult', TYPE],
    ['ReadableWritablePair', TYPE],
    ['RegistrationOptions', TYPE],
    ['ReportingObserverOptions', TYPE],
    ['RequestInit', TYPE],
    ['ResponseInit', TYPE],
    ['RsaHashedImportParams', TYPE],
    ['RsaHashedKeyGenParams', TYPE],
    ['RsaKeyGenParams', TYPE],
    ['RsaOaepParams', TYPE],
    ['RsaOtherPrimesInfo', TYPE],
    ['RsaPssParams', TYPE],
    ['SecurityPolicyViolationEventInit', TYPE],
    ['StorageEstimate', TYPE],
    ['StreamPipeOptions', TYPE],
    ['StructuredSerializeOptions', TYPE],
    ['TextDecodeOptions', TYPE],
    ['TextDecoderOptions', TYPE],
    ['TextEncoderEncodeIntoResult', TYPE],
    ['Transformer', TYPE],
    ['UnderlyingByteSource', TYPE],
    ['UnderlyingDefaultSource', TYPE],
    ['UnderlyingSink', TYPE],
    ['UnderlyingSource', TYPE],
    ['VideoColorSpaceInit', TYPE],
    ['VideoConfiguration', TYPE],
    ['VideoDecoderConfig', TYPE],
    ['VideoDecoderInit', TYPE],
    ['VideoDecoderSupport', TYPE],
    ['VideoEncoderConfig', TYPE],
    ['VideoEncoderEncodeOptions', TYPE],
    ['VideoEncoderEncodeOptionsForAvc', TYPE],
    ['VideoEncoderInit', TYPE],
    ['VideoEncoderSupport', TYPE],
    ['VideoFrameBufferInit', TYPE],
    ['VideoFrameCopyToOptions', TYPE],
    ['VideoFrameInit', TYPE],
    ['WebGLContextAttributes', TYPE],
    ['WebGLContextEventInit', TYPE],
    ['WebTransportCloseInfo', TYPE],
    ['WebTransportErrorOptions', TYPE],
    ['WebTransportHash', TYPE],
    ['WebTransportOptions', TYPE],
    ['WebTransportSendStreamOptions', TYPE],
    ['WorkerOptions', TYPE],
    ['WriteParams', TYPE],
    ['ANGLE_instanced_arrays', TYPE],
    ['AbortController', TYPE_VALUE],
    ['AbortSignalEventMap', TYPE],
    ['AbortSignal', TYPE_VALUE],
    ['AbstractWorkerEventMap', TYPE],
    ['AbstractWorker', TYPE],
    ['AnimationFrameProvider', TYPE],
    ['AudioData', TYPE_VALUE],
    ['AudioDecoderEventMap', TYPE],
    ['AudioDecoder', TYPE_VALUE],
    ['AudioEncoderEventMap', TYPE],
    ['AudioEncoder', TYPE_VALUE],
    ['Blob', TYPE_VALUE],
    ['Body', TYPE],
    ['BroadcastChannelEventMap', TYPE],
    ['BroadcastChannel', TYPE_VALUE],
    ['ByteLengthQueuingStrategy', TYPE_VALUE],
    ['CSSImageValue', TYPE_VALUE],
    ['CSSKeywordValue', TYPE_VALUE],
    ['CSSMathClamp', TYPE_VALUE],
    ['CSSMathInvert', TYPE_VALUE],
    ['CSSMathMax', TYPE_VALUE],
    ['CSSMathMin', TYPE_VALUE],
    ['CSSMathNegate', TYPE_VALUE],
    ['CSSMathProduct', TYPE_VALUE],
    ['CSSMathSum', TYPE_VALUE],
    ['CSSMathValue', TYPE_VALUE],
    ['CSSMatrixComponent', TYPE_VALUE],
    ['CSSNumericArray', TYPE_VALUE],
    ['CSSNumericValue', TYPE_VALUE],
    ['CSSPerspective', TYPE_VALUE],
    ['CSSRotate', TYPE_VALUE],
    ['CSSScale', TYPE_VALUE],
    ['CSSSkew', TYPE_VALUE],
    ['CSSSkewX', TYPE_VALUE],
    ['CSSSkewY', TYPE_VALUE],
    ['CSSStyleValue', TYPE_VALUE],
    ['CSSTransformComponent', TYPE_VALUE],
    ['CSSTransformValue', TYPE_VALUE],
    ['CSSTranslate', TYPE_VALUE],
    ['CSSUnitValue', TYPE_VALUE],
    ['CSSUnparsedValue', TYPE_VALUE],
    ['CSSVariableReferenceValue', TYPE_VALUE],
    ['Cache', TYPE_VALUE],
    ['CacheStorage', TYPE_VALUE],
    ['CanvasCompositing', TYPE],
    ['CanvasDrawImage', TYPE],
    ['CanvasDrawPath', TYPE],
    ['CanvasFillStrokeStyles', TYPE],
    ['CanvasFilters', TYPE],
    ['CanvasGradient', TYPE_VALUE],
    ['CanvasImageData', TYPE],
    ['CanvasImageSmoothing', TYPE],
    ['CanvasPath', TYPE],
    ['CanvasPathDrawingStyles', TYPE],
    ['CanvasPattern', TYPE_VALUE],
    ['CanvasRect', TYPE],
    ['CanvasShadowStyles', TYPE],
    ['CanvasState', TYPE],
    ['CanvasText', TYPE],
    ['CanvasTextDrawingStyles', TYPE],
    ['CanvasTransform', TYPE],
    ['Client', TYPE_VALUE],
    ['Clients', TYPE_VALUE],
    ['CloseEvent', TYPE_VALUE],
    ['CompressionStream', TYPE_VALUE],
    ['CountQueuingStrategy', TYPE_VALUE],
    ['Crypto', TYPE_VALUE],
    ['CryptoKey', TYPE_VALUE],
    ['CustomEvent', TYPE_VALUE],
    ['DOMException', TYPE_VALUE],
    ['DOMMatrix', TYPE_VALUE],
    ['DOMMatrixReadOnly', TYPE_VALUE],
    ['DOMPoint', TYPE_VALUE],
    ['DOMPointReadOnly', TYPE_VALUE],
    ['DOMQuad', TYPE_VALUE],
    ['DOMRect', TYPE_VALUE],
    ['DOMRectReadOnly', TYPE_VALUE],
    ['DOMStringList', TYPE_VALUE],
    ['DecompressionStream', TYPE_VALUE],
    ['DedicatedWorkerGlobalScopeEventMap', TYPE],
    ['DedicatedWorkerGlobalScope', TYPE_VALUE],
    ['EXT_blend_minmax', TYPE],
    ['EXT_color_buffer_float', TYPE],
    ['EXT_color_buffer_half_float', TYPE],
    ['EXT_float_blend', TYPE],
    ['EXT_frag_depth', TYPE],
    ['EXT_sRGB', TYPE],
    ['EXT_shader_texture_lod', TYPE],
    ['EXT_texture_compression_bptc', TYPE],
    ['EXT_texture_compression_rgtc', TYPE],
    ['EXT_texture_filter_anisotropic', TYPE],
    ['EXT_texture_norm16', TYPE],
    ['EncodedAudioChunk', TYPE_VALUE],
    ['EncodedVideoChunk', TYPE_VALUE],
    ['ErrorEvent', TYPE_VALUE],
    ['Event', TYPE_VALUE],
    ['EventListener', TYPE],
    ['EventListenerObject', TYPE],
    ['EventSourceEventMap', TYPE],
    ['EventSource', TYPE_VALUE],
    ['EventTarget', TYPE_VALUE],
    ['ExtendableEvent', TYPE_VALUE],
    ['ExtendableMessageEvent', TYPE_VALUE],
    ['FetchEvent', TYPE_VALUE],
    ['File', TYPE_VALUE],
    ['FileList', TYPE_VALUE],
    ['FileReaderEventMap', TYPE],
    ['FileReader', TYPE_VALUE],
    ['FileReaderSync', TYPE_VALUE],
    ['FileSystemDirectoryHandle', TYPE_VALUE],
    ['FileSystemFileHandle', TYPE_VALUE],
    ['FileSystemHandle', TYPE_VALUE],
    ['FileSystemSyncAccessHandle', TYPE_VALUE],
    ['FileSystemWritableFileStream', TYPE_VALUE],
    ['FontFace', TYPE_VALUE],
    ['FontFaceSetEventMap', TYPE],
    ['FontFaceSet', TYPE_VALUE],
    ['FontFaceSetLoadEvent', TYPE_VALUE],
    ['FontFaceSource', TYPE],
    ['FormData', TYPE_VALUE],
    ['GPUError', TYPE],
    ['GenericTransformStream', TYPE],
    ['Headers', TYPE_VALUE],
    ['IDBCursor', TYPE_VALUE],
    ['IDBCursorWithValue', TYPE_VALUE],
    ['IDBDatabaseEventMap', TYPE],
    ['IDBDatabase', TYPE_VALUE],
    ['IDBFactory', TYPE_VALUE],
    ['IDBIndex', TYPE_VALUE],
    ['IDBKeyRange', TYPE_VALUE],
    ['IDBObjectStore', TYPE_VALUE],
    ['IDBOpenDBRequestEventMap', TYPE],
    ['IDBOpenDBRequest', TYPE_VALUE],
    ['IDBRequestEventMap', TYPE],
    ['IDBRequest', TYPE_VALUE],
    ['IDBTransactionEventMap', TYPE],
    ['IDBTransaction', TYPE_VALUE],
    ['IDBVersionChangeEvent', TYPE_VALUE],
    ['ImageBitmap', TYPE_VALUE],
    ['ImageBitmapRenderingContext', TYPE_VALUE],
    ['ImageData', TYPE_VALUE],
    ['ImageDecoder', TYPE_VALUE],
    ['ImageTrack', TYPE_VALUE],
    ['ImageTrackList', TYPE_VALUE],
    ['ImportMeta', TYPE],
    ['KHR_parallel_shader_compile', TYPE],
    ['Lock', TYPE_VALUE],
    ['LockManager', TYPE_VALUE],
    ['MediaCapabilities', TYPE_VALUE],
    ['MediaSourceHandle', TYPE_VALUE],
    ['MediaStreamTrackProcessor', TYPE_VALUE],
    ['MessageChannel', TYPE_VALUE],
    ['MessageEvent', TYPE_VALUE],
    ['MessageEventTargetEventMap', TYPE],
    ['MessageEventTarget', TYPE],
    ['MessagePortEventMap', TYPE],
    ['MessagePort', TYPE_VALUE],
    ['NavigationPreloadManager', TYPE_VALUE],
    ['NavigatorBadge', TYPE],
    ['NavigatorConcurrentHardware', TYPE],
    ['NavigatorID', TYPE],
    ['NavigatorLanguage', TYPE],
    ['NavigatorLocks', TYPE],
    ['NavigatorOnLine', TYPE],
    ['NavigatorStorage', TYPE],
    ['NotificationEventMap', TYPE],
    ['Notification', TYPE_VALUE],
    ['NotificationEvent', TYPE_VALUE],
    ['OES_draw_buffers_indexed', TYPE],
    ['OES_element_index_uint', TYPE],
    ['OES_fbo_render_mipmap', TYPE],
    ['OES_standard_derivatives', TYPE],
    ['OES_texture_float', TYPE],
    ['OES_texture_float_linear', TYPE],
    ['OES_texture_half_float', TYPE],
    ['OES_texture_half_float_linear', TYPE],
    ['OES_vertex_array_object', TYPE],
    ['OVR_multiview2', TYPE],
    ['OffscreenCanvasEventMap', TYPE],
    ['OffscreenCanvas', TYPE_VALUE],
    ['OffscreenCanvasRenderingContext2D', TYPE_VALUE],
    ['Path2D', TYPE_VALUE],
    ['PerformanceEventMap', TYPE],
    ['Performance', TYPE_VALUE],
    ['PerformanceEntry', TYPE_VALUE],
    ['PerformanceMark', TYPE_VALUE],
    ['PerformanceMeasure', TYPE_VALUE],
    ['PerformanceObserver', TYPE_VALUE],
    ['PerformanceObserverEntryList', TYPE_VALUE],
    ['PerformanceResourceTiming', TYPE_VALUE],
    ['PerformanceServerTiming', TYPE_VALUE],
    ['PermissionStatusEventMap', TYPE],
    ['PermissionStatus', TYPE_VALUE],
    ['Permissions', TYPE_VALUE],
    ['ProgressEvent', TYPE_VALUE],
    ['PromiseRejectionEvent', TYPE_VALUE],
    ['PushEvent', TYPE_VALUE],
    ['PushManager', TYPE_VALUE],
    ['PushMessageData', TYPE_VALUE],
    ['PushSubscription', TYPE_VALUE],
    ['PushSubscriptionOptions', TYPE_VALUE],
    ['RTCDataChannelEventMap', TYPE],
    ['RTCDataChannel', TYPE_VALUE],
    ['RTCEncodedAudioFrame', TYPE_VALUE],
    ['RTCEncodedVideoFrame', TYPE_VALUE],
    ['RTCRtpScriptTransformer', TYPE_VALUE],
    ['RTCTransformEvent', TYPE_VALUE],
    ['ReadableByteStreamController', TYPE_VALUE],
    ['ReadableStream', TYPE_VALUE],
    ['ReadableStreamBYOBReader', TYPE_VALUE],
    ['ReadableStreamBYOBRequest', TYPE_VALUE],
    ['ReadableStreamDefaultController', TYPE_VALUE],
    ['ReadableStreamDefaultReader', TYPE_VALUE],
    ['ReadableStreamGenericReader', TYPE],
    ['Report', TYPE_VALUE],
    ['ReportBody', TYPE_VALUE],
    ['ReportingObserver', TYPE_VALUE],
    ['Request', TYPE_VALUE],
    ['Response', TYPE_VALUE],
    ['SecurityPolicyViolationEvent', TYPE_VALUE],
    ['ServiceWorkerEventMap', TYPE],
    ['ServiceWorker', TYPE_VALUE],
    ['ServiceWorkerContainerEventMap', TYPE],
    ['ServiceWorkerContainer', TYPE_VALUE],
    ['ServiceWorkerGlobalScopeEventMap', TYPE],
    ['ServiceWorkerGlobalScope', TYPE_VALUE],
    ['ServiceWorkerRegistrationEventMap', TYPE],
    ['ServiceWorkerRegistration', TYPE_VALUE],
    ['SharedWorkerGlobalScopeEventMap', TYPE],
    ['SharedWorkerGlobalScope', TYPE_VALUE],
    ['StorageManager', TYPE_VALUE],
    ['StylePropertyMapReadOnly', TYPE_VALUE],
    ['SubtleCrypto', TYPE_VALUE],
    ['TextDecoder', TYPE_VALUE],
    ['TextDecoderCommon', TYPE],
    ['TextDecoderStream', TYPE_VALUE],
    ['TextEncoder', TYPE_VALUE],
    ['TextEncoderCommon', TYPE],
    ['TextEncoderStream', TYPE_VALUE],
    ['TextMetrics', TYPE_VALUE],
    ['TransformStream', TYPE_VALUE],
    ['TransformStreamDefaultController', TYPE_VALUE],
    ['URL', TYPE_VALUE],
    ['URLSearchParams', TYPE_VALUE],
    ['VideoColorSpace', TYPE_VALUE],
    ['VideoDecoderEventMap', TYPE],
    ['VideoDecoder', TYPE_VALUE],
    ['VideoEncoderEventMap', TYPE],
    ['VideoEncoder', TYPE_VALUE],
    ['VideoFrame', TYPE_VALUE],
    ['WEBGL_color_buffer_float', TYPE],
    ['WEBGL_compressed_texture_astc', TYPE],
    ['WEBGL_compressed_texture_etc', TYPE],
    ['WEBGL_compressed_texture_etc1', TYPE],
    ['WEBGL_compressed_texture_pvrtc', TYPE],
    ['WEBGL_compressed_texture_s3tc', TYPE],
    ['WEBGL_compressed_texture_s3tc_srgb', TYPE],
    ['WEBGL_debug_renderer_info', TYPE],
    ['WEBGL_debug_shaders', TYPE],
    ['WEBGL_depth_texture', TYPE],
    ['WEBGL_draw_buffers', TYPE],
    ['WEBGL_lose_context', TYPE],
    ['WEBGL_multi_draw', TYPE],
    ['WebGL2RenderingContext', TYPE_VALUE],
    ['WebGL2RenderingContextBase', TYPE],
    ['WebGL2RenderingContextOverloads', TYPE],
    ['WebGLActiveInfo', TYPE_VALUE],
    ['WebGLBuffer', TYPE_VALUE],
    ['WebGLContextEvent', TYPE_VALUE],
    ['WebGLFramebuffer', TYPE_VALUE],
    ['WebGLProgram', TYPE_VALUE],
    ['WebGLQuery', TYPE_VALUE],
    ['WebGLRenderbuffer', TYPE_VALUE],
    ['WebGLRenderingContext', TYPE_VALUE],
    ['WebGLRenderingContextBase', TYPE],
    ['WebGLRenderingContextOverloads', TYPE],
    ['WebGLSampler', TYPE_VALUE],
    ['WebGLShader', TYPE_VALUE],
    ['WebGLShaderPrecisionFormat', TYPE_VALUE],
    ['WebGLSync', TYPE_VALUE],
    ['WebGLTexture', TYPE_VALUE],
    ['WebGLTransformFeedback', TYPE_VALUE],
    ['WebGLUniformLocation', TYPE_VALUE],
    ['WebGLVertexArrayObject', TYPE_VALUE],
    ['WebGLVertexArrayObjectOES', TYPE],
    ['WebSocketEventMap', TYPE],
    ['WebSocket', TYPE_VALUE],
    ['WebTransport', TYPE_VALUE],
    ['WebTransportBidirectionalStream', TYPE_VALUE],
    ['WebTransportDatagramDuplexStream', TYPE_VALUE],
    ['WebTransportError', TYPE_VALUE],
    ['WindowClient', TYPE_VALUE],
    ['WindowOrWorkerGlobalScope', TYPE],
    ['WorkerEventMap', TYPE],
    ['Worker', TYPE_VALUE],
    ['WorkerGlobalScopeEventMap', TYPE],
    ['WorkerGlobalScope', TYPE_VALUE],
    ['WorkerLocation', TYPE_VALUE],
    ['WorkerNavigator', TYPE_VALUE],
    ['WritableStream', TYPE_VALUE],
    ['WritableStreamDefaultController', TYPE_VALUE],
    ['WritableStreamDefaultWriter', TYPE_VALUE],
    ['XMLHttpRequestEventMap', TYPE],
    ['XMLHttpRequest', TYPE_VALUE],
    ['XMLHttpRequestEventTargetEventMap', TYPE],
    ['XMLHttpRequestEventTarget', TYPE_VALUE],
    ['XMLHttpRequestUpload', TYPE_VALUE],
    ['Console', TYPE],
    ['WebAssembly', TYPE_VALUE],
    ['AudioDataOutputCallback', TYPE],
    ['EncodedAudioChunkOutputCallback', TYPE],
    ['EncodedVideoChunkOutputCallback', TYPE],
    ['FrameRequestCallback', TYPE],
    ['LockGrantedCallback', TYPE],
    ['OnErrorEventHandlerNonNull', TYPE],
    ['PerformanceObserverCallback', TYPE],
    ['QueuingStrategySize', TYPE],
    ['ReportingObserverCallback', TYPE],
    ['TransformerFlushCallback', TYPE],
    ['TransformerStartCallback', TYPE],
    ['TransformerTransformCallback', TYPE],
    ['UnderlyingSinkAbortCallback', TYPE],
    ['UnderlyingSinkCloseCallback', TYPE],
    ['UnderlyingSinkStartCallback', TYPE],
    ['UnderlyingSinkWriteCallback', TYPE],
    ['UnderlyingSourceCancelCallback', TYPE],
    ['UnderlyingSourcePullCallback', TYPE],
    ['UnderlyingSourceStartCallback', TYPE],
    ['VideoFrameOutputCallback', TYPE],
    ['VoidFunction', TYPE],
    ['WebCodecsErrorCallback', TYPE],
    ['AlgorithmIdentifier', TYPE],
    ['AllowSharedBufferSource', TYPE],
    ['BigInteger', TYPE],
    ['BlobPart', TYPE],
    ['BodyInit', TYPE],
    ['BufferSource', TYPE],
    ['CSSKeywordish', TYPE],
    ['CSSNumberish', TYPE],
    ['CSSPerspectiveValue', TYPE],
    ['CSSUnparsedSegment', TYPE],
    ['CanvasImageSource', TYPE],
    ['DOMHighResTimeStamp', TYPE],
    ['EpochTimeStamp', TYPE],
    ['EventListenerOrEventListenerObject', TYPE],
    ['FileSystemWriteChunkType', TYPE],
    ['Float32List', TYPE],
    ['FormDataEntryValue', TYPE],
    ['GLbitfield', TYPE],
    ['GLboolean', TYPE],
    ['GLclampf', TYPE],
    ['GLenum', TYPE],
    ['GLfloat', TYPE],
    ['GLint', TYPE],
    ['GLint64', TYPE],
    ['GLintptr', TYPE],
    ['GLsizei', TYPE],
    ['GLsizeiptr', TYPE],
    ['GLuint', TYPE],
    ['GLuint64', TYPE],
    ['HashAlgorithmIdentifier', TYPE],
    ['HeadersInit', TYPE],
    ['IDBValidKey', TYPE],
    ['ImageBitmapSource', TYPE],
    ['ImageBufferSource', TYPE],
    ['Int32List', TYPE],
    ['MessageEventSource', TYPE],
    ['NamedCurve', TYPE],
    ['OffscreenRenderingContext', TYPE],
    ['OnErrorEventHandler', TYPE],
    ['PerformanceEntryList', TYPE],
    ['PushMessageDataInit', TYPE],
    ['ReadableStreamController', TYPE],
    ['ReadableStreamReadResult', TYPE],
    ['ReadableStreamReader', TYPE],
    ['ReportList', TYPE],
    ['RequestInfo', TYPE],
    ['TexImageSource', TYPE],
    ['TimerHandler', TYPE],
    ['Transferable', TYPE],
    ['Uint32List', TYPE],
    ['XMLHttpRequestBodyInit', TYPE],
    ['AlphaOption', TYPE],
    ['AudioSampleFormat', TYPE],
    ['AvcBitstreamFormat', TYPE],
    ['BinaryType', TYPE],
    ['BitrateMode', TYPE],
    ['CSSMathOperator', TYPE],
    ['CSSNumericBaseType', TYPE],
    ['CanvasDirection', TYPE],
    ['CanvasFillRule', TYPE],
    ['CanvasFontKerning', TYPE],
    ['CanvasFontStretch', TYPE],
    ['CanvasFontVariantCaps', TYPE],
    ['CanvasLineCap', TYPE],
    ['CanvasLineJoin', TYPE],
    ['CanvasTextAlign', TYPE],
    ['CanvasTextBaseline', TYPE],
    ['CanvasTextRendering', TYPE],
    ['ClientTypes', TYPE],
    ['CodecState', TYPE],
    ['ColorGamut', TYPE],
    ['ColorSpaceConversion', TYPE],
    ['CompressionFormat', TYPE],
    ['DocumentVisibilityState', TYPE],
    ['EncodedAudioChunkType', TYPE],
    ['EncodedVideoChunkType', TYPE],
    ['EndingType', TYPE],
    ['FileSystemHandleKind', TYPE],
    ['FontDisplay', TYPE],
    ['FontFaceLoadStatus', TYPE],
    ['FontFaceSetLoadStatus', TYPE],
    ['FrameType', TYPE],
    ['GlobalCompositeOperation', TYPE],
    ['HardwareAcceleration', TYPE],
    ['HdrMetadataType', TYPE],
    ['IDBCursorDirection', TYPE],
    ['IDBRequestReadyState', TYPE],
    ['IDBTransactionDurability', TYPE],
    ['IDBTransactionMode', TYPE],
    ['ImageOrientation', TYPE],
    ['ImageSmoothingQuality', TYPE],
    ['KeyFormat', TYPE],
    ['KeyType', TYPE],
    ['KeyUsage', TYPE],
    ['LatencyMode', TYPE],
    ['LockMode', TYPE],
    ['MediaDecodingType', TYPE],
    ['MediaEncodingType', TYPE],
    ['NotificationDirection', TYPE],
    ['NotificationPermission', TYPE],
    ['OffscreenRenderingContextId', TYPE],
    ['OpusBitstreamFormat', TYPE],
    ['PermissionName', TYPE],
    ['PermissionState', TYPE],
    ['PredefinedColorSpace', TYPE],
    ['PremultiplyAlpha', TYPE],
    ['PushEncryptionKeyName', TYPE],
    ['RTCDataChannelState', TYPE],
    ['RTCEncodedVideoFrameType', TYPE],
    ['ReadableStreamReaderMode', TYPE],
    ['ReadableStreamType', TYPE],
    ['ReferrerPolicy', TYPE],
    ['RequestCache', TYPE],
    ['RequestCredentials', TYPE],
    ['RequestDestination', TYPE],
    ['RequestMode', TYPE],
    ['RequestPriority', TYPE],
    ['RequestRedirect', TYPE],
    ['ResizeQuality', TYPE],
    ['ResponseType', TYPE],
    ['SecurityPolicyViolationEventDisposition', TYPE],
    ['ServiceWorkerState', TYPE],
    ['ServiceWorkerUpdateViaCache', TYPE],
    ['TransferFunction', TYPE],
    ['VideoColorPrimaries', TYPE],
    ['VideoEncoderBitrateMode', TYPE],
    ['VideoMatrixCoefficients', TYPE],
    ['VideoPixelFormat', TYPE],
    ['VideoTransferCharacteristics', TYPE],
    ['WebGLPowerPreference', TYPE],
    ['WebTransportCongestionControl', TYPE],
    ['WebTransportErrorSource', TYPE],
    ['WorkerType', TYPE],
    ['WriteCommandType', TYPE],
    ['XMLHttpRequestResponseType', TYPE],
  ],
}` | ✓ |


---