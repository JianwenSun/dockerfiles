FROM ubuntu:16.04  
  
ENV CANTALOUPE_UID=999 \  
CANTALOUPE_GID=999 \  
JAVA_OPTS=-Xmx500m \  
PROPERTIES_FILE=/cantaloupe/cantaloupe.properties \  
HTTP_HTTP2_ENABLED=false \  
HTTP_ACCEPT_QUEUE_LIMIT=0 \  
BASE_URI= \  
SLASH_SUBSTITUTE= \  
MAX_PIXELS=400000000 \  
PRINT_STACK_TRACE_ON_ERROR_PAGES=true \  
DELEGATE_SCRIPT_ENABLED=false \  
DELEGATE_SCRIPT_PATHNAME=delegates-3.4.rb \  
DELEGATE_SCRIPT_CACHE_ENABLED=false \  
ENDPOINT_PUBLIC_AUTH_BASIC_ENABLED=false \  
ENDPOINT_PUBLIC_AUTH_BASIC_USERNAME=myself \  
ENDPOINT_PUBLIC_AUTH_BASIC_SECRET=mypassword \  
ENDPOINT_IIIF_1_ENABLED=true \  
ENDPOINT_IIIF_2_ENABLED=true \  
ENDPOINT_IIIF_CONTENT_DISPOSITION=none \  
ENDPOINT_IIIF_MIN_SIZE=64 \  
ENDPOINT_IIIF_MIN_TILE_SIZE=1024 \  
ENDPOINT_IIIF_2_RESTRICT_TO_SIZES=false \  
ENDPOINT_ADMIN_ENABLED=false \  
ENDPOINT_ADMIN_USERNAME=admin \  
ENDPOINT_ADMIN_SECRET= \  
ENDPOINT_API_ENABLED=false \  
ENDPOINT_API_USERNAME= \  
ENDPOINT_API_SECRET= \  
RESOLVER_STATIC=FilesystemResolver \  
RESOLVER_DELEGATE=false \  
FILESYSTEMRESOLVER_LOOKUP_STRATEGY=BasicLookupStrategy \  
FILESYSTEMRESOLVER_BASICLOOKUPSTRATEGY_PATH_PREFIX=/cantaloupe/images \  
FILESYSTEMRESOLVER_BASICLOOKUPSTRATEGY_PATH_SUFFIX= \  
HTTPRESOLVER_TRUST_ALL_CERTS=false \  
HTTPRESOLVER_REQUEST_TIMEOUT=10 \  
HTTPRESOLVER_LOOKUP_STRATEGY=BasicLookupStrategy \  
HTTPRESOLVER_BASICLOOKUPSTRATEGY_URL_PREFIX=http://localhost/images/ \  
HTTPRESOLVER_BASICLOOKUPSTRATEGY_URL_SUFFIX= \  
HTTPRESOLVER_AUTH_BASIC_USERNAME= \  
HTTPRESOLVER_AUTH_BASIC_SECRET= \  
JDBCRESOLVER_URL=jdbc:postgresql://localhost:5432/my_database \  
JDBCRESOLVER_USER=postgres \  
JDBCRESOLVER_PASSWORD=postgres \  
JDBCRESOLVER_CONNECTION_TIMEOUT=10 \  
AMAZONS3RESOLVER_ACCESS_KEY_ID= \  
AMAZONS3RESOLVER_SECRET_KEY= \  
AMAZONS3RESOLVER_BUCKET_NAME= \  
AMAZONS3RESOLVER_BUCKET_REGION= \  
AMAZONS3RESOLVER_LOOKUP_STRATEGY=BasicLookupStrategy \  
AMAZONS3RESOLVER_MAX_CONNECTIONS= \  
AZURESTORAGERESOLVER_ACCOUNT_NAME= \  
AZURESTORAGERESOLVER_ACCOUNT_KEY= \  
AZURESTORAGERESOLVER_CONTAINER_NAME= \  
AZURESTORAGERESOLVER_LOOKUP_STRATEGY=BasicLookupStrategy \  
PROCESSOR_AVI=FfmpegProcessor \  
PROCESSOR_BMP= \  
PROCESSOR_DCM=ImageMagickProcessor \  
PROCESSOR_FLV=FfmpegProcessor \  
PROCESSOR_GIF= \  
PROCESSOR_JP2=KakaduProcessor \  
PROCESSOR_JPG= \  
PROCESSOR_MOV=FfmpegProcessor \  
PROCESSOR_MP4=FfmpegProcessor \  
PROCESSOR_MPG=FfmpegProcessor \  
PROCESSOR_PDF=PdfBoxProcessor \  
PROCESSOR_PNG= \  
PROCESSOR_TIF= \  
PROCESSOR_WEBM=FfmpegProcessor \  
PROCESSOR_WEBP=ImageMagickProcessor \  
PROCESSOR_FALLBACK=Java2dProcessor \  
PROCESSOR_DPI=150 \  
PROCESSOR_NORMALIZE=false \  
PROCESSOR_BACKGROUND_COLOR=black \  
PROCESSOR_DOWNSCALE_FILTER=bicubic \  
PROCESSOR_UPSCALE_FILTER=bicubic \  
PROCESSOR_SHARPEN=0 \  
PROCESSOR_METADATA_PRESERVE=false \  
PROCESSOR_METADATA_RESPECT_ORIENTATION=false \  
PROCESSOR_LIMIT_TO_8_BITS=true \  
PROCESSOR_JPG_PROGRESSIVE=true \  
PROCESSOR_JPG_QUALITY=80 \  
PROCESSOR_TIF_COMPRESSION=LZW \  
STREAMPROCESSOR_RETRIEVAL_STRATEGY=StreamStrategy \  
CACHE_CLIENT_ENABLED=true \  
CACHE_CLIENT_MAX_AGE=2592000 \  
CACHE_CLIENT_SHARED_MAX_AGE= \  
CACHE_CLIENT_PUBLIC=true \  
CACHE_CLIENT_PRIVATE=false \  
CACHE_CLIENT_NO_CACHE=false \  
CACHE_CLIENT_NO_STORE=false \  
CACHE_CLIENT_MUST_REVALIDATE=false \  
CACHE_CLIENT_PROXY_REVALIDATE=false \  
CACHE_CLIENT_NO_TRANSFORM=true \  
CACHE_SERVER_SOURCE_ENABLED=false \  
CACHE_SERVER_SOURCE=FilesystemCache \  
CACHE_SERVER_DERIVATIVE_ENABLED=false \  
CACHE_SERVER_DERIVATIVE= \  
CACHE_SERVER_INFO_ENABLED=true \  
CACHE_SERVER_TTL_SECONDS=2592000 \  
CACHE_SERVER_PURGE_MISSING=false \  
CACHE_SERVER_RESOLVE_FIRST=false \  
CACHE_SERVER_WORKER_ENABLED=false \  
CACHE_SERVER_WORKER_INTERVAL=86400 \  
FILESYSTEMCACHE_PATHNAME=/cantaloupe/cache \  
FILESYSTEMCACHE_DIR_DEPTH=3 \  
FILESYSTEMCACHE_DIR_NAME_LENGTH=2 \  
HEAPCACHE_TARGET_SIZE=2G \  
HEAPCACHE_PERSIST=false \  
HEAPCACHE_PERSIST_FILESYSTEM_PATHNAME=/var/cache/cantaloupe/heap.cache \  
JDBCCACHE_URL=jdbc:postgresql://localhost:5432/cantaloupe \  
JDBCCACHE_USER=postgres \  
JDBCCACHE_PASSWORD= \  
JDBCCACHE_CONNECTION_TIMEOUT=10 \  
JDBCCACHE_DERIVATIVE_IMAGE_TABLE=derivative_cache \  
JDBCCACHE_INFO_TABLE=info_cache \  
AMAZONS3CACHE_ACCESS_KEY_ID= \  
AMAZONS3CACHE_SECRET_KEY= \  
AMAZONS3CACHE_BUCKET_NAME= \  
AMAZONS3CACHE_BUCKET_REGION= \  
AMAZONS3CACHE_OBJECT_KEY_PREFIX= \  
AMAZONS3CACHE_MAX_CONNECTIONS= \  
AZURESTORAGECACHE_ACCOUNT_NAME= \  
AZURESTORAGECACHE_ACCOUNT_KEY= \  
AZURESTORAGECACHE_CONTAINER_NAME= \  
AZURESTORAGECACHE_OBJECT_KEY_PREFIX= \  
REDISCACHE_HOST=localhost \  
REDISCACHE_PORT=6379 \  
REDISCACHE_SSL=false \  
REDISCACHE_PASSWORD= \  
REDISCACHE_DATABASE=0 \  
OVERLAYS_ENABLED=false \  
OVERLAYS_STRATEGY=BasicStrategy \  
OVERLAYS_BASICSTRATEGY_TYPE=image \  
OVERLAYS_BASICSTRATEGY_IMAGE=/path/to/overlay.png \  
OVERLAYS_BASICSTRATEGY_STRING="Copyright \u00A9️ My Great Organization\nAll
rights reserved." \  
OVERLAYS_BASICSTRATEGY_STRING_FONT=Helvetica \  
OVERLAYS_BASICSTRATEGY_STRING_FONT_SIZE=24 \  
OVERLAYS_BASICSTRATEGY_STRING_FONT_MIN_SIZE=18 \  
OVERLAYS_BASICSTRATEGY_STRING_FONT_WEIGHT=1.0 \  
OVERLAYS_BASICSTRATEGY_STRING_GLYPH_SPACING=0.02 \  
OVERLAYS_BASICSTRATEGY_STRING_COLOR=white \  
OVERLAYS_BASICSTRATEGY_STRING_STROKE_COLOR=black \  
OVERLAYS_BASICSTRATEGY_STRING_STROKE_WIDTH=1 \  
OVERLAYS_BASICSTRATEGY_STRING_BACKGROUND_COLOR="rgba(0, 0, 0, 100)" \  
OVERLAYS_BASICSTRATEGY_POSITION="bottom right" \  
OVERLAYS_BASICSTRATEGY_INSET=10 \  
OVERLAYS_BASICSTRATEGY_OUTPUT_WIDTH_THRESHOLD=400 \  
OVERLAYS_BASICSTRATEGY_OUTPUT_HEIGHT_THRESHOLD=300 \  
REDACTION_ENABLED=false \  
LOG_APPLICATION_LEVEL=debug \  
LOG_APPLICATION_CONSOLEAPPENDER_ENABLED=true \  
LOG_APPLICATION_FILEAPPENDER_ENABLED=false \  
LOG_APPLICATION_FILEAPPENDER_PATHNAME=/cantaloupe/logs/application.log \  
LOG_APPLICATION_ROLLINGFILEAPPENDER_ENABLED=false \  
LOG_APPLICATION_ROLLINGFILEAPPENDER_PATHNAME=/cantaloupe/logs/application.log
\  
LOG_APPLICATION_ROLLINGFILEAPPENDER_POLICY=TimeBasedRollingPolicy \  
LOG_APPLICATION_ROLLINGFILEAPPENDER_TIMEBASEDROLLINGPOLICY_FILENAME_PATTERN=/path/to/logs/application-%d{yyyy-
MM-dd}.log \  
LOG_APPLICATION_ROLLINGFILEAPPENDER_TIMEBASEDROLLINGPOLICY_MAX_HISTORY=30 \  
LOG_APPLICATION_SYSLOGAPPENDER_ENABLED=false \  
LOG_APPLICATION_SYSLOGAPPENDER_HOST= \  
LOG_APPLICATION_SYSLOGAPPENDER_PORT=514 \  
LOG_APPLICATION_SYSLOGAPPENDER_FACILITY=LOCAL0 \  
LOG_ERROR_FILEAPPENDER_ENABLED=false \  
LOG_ERROR_FILEAPPENDER_PATHNAME=/cantaloupe/logs/error.log \  
LOG_ERROR_ROLLINGFILEAPPENDER_ENABLED=false \  
LOG_ERROR_ROLLINGFILEAPPENDER_PATHNAME=/cantaloupe/logs/error.log \  
LOG_ERROR_ROLLINGFILEAPPENDER_POLICY=TimeBasedRollingPolicy \  
LOG_ERROR_ROLLINGFILEAPPENDER_TIMEBASEDROLLINGPOLICY_FILENAME_PATTERN=/path/to/logs/error-%d{yyyy-
MM-dd}.log \  
LOG_ERROR_ROLLINGFILEAPPENDER_TIMEBASEDROLLINGPOLICY_MAX_HISTORY=30 \  
LOG_ACCESS_CONSOLEAPPENDER_ENABLED=false \  
LOG_ACCESS_FILEAPPENDER_ENABLED=false \  
LOG_ACCESS_FILEAPPENDER_PATHNAME=/cantaloupe/logs/access.log \  
LOG_ACCESS_ROLLINGFILEAPPENDER_ENABLED=false \  
LOG_ACCESS_ROLLINGFILEAPPENDER_PATHNAME=/cantaloupe/logs/access.log \  
LOG_ACCESS_ROLLINGFILEAPPENDER_POLICY=TimeBasedRollingPolicy \  
LOG_ACCESS_ROLLINGFILEAPPENDER_TIMEBASEDROLLINGPOLICY_FILENAME_PATTERN=/path/to/logs/access-%d{yyyy-
MM-dd}.log \  
LOG_ACCESS_ROLLINGFILEAPPENDER_TIMEBASEDROLLINGPOLICY_MAX_HISTORY=30 \  
LOG_ACCESS_SYSLOGAPPENDER_ENABLED=false \  
LOG_ACCESS_SYSLOGAPPENDER_HOST= \  
LOG_ACCESS_SYSLOGAPPENDER_PORT=514 \  
LOG_ACCESS_SYSLOGAPPENDER_FACILITY=LOCAL0  
  
COPY . /build  
RUN /build/setup.sh  
  
EXPOSE 8182  
WORKDIR /cantaloupe  
HEALTHCHECK CMD curl --fail http://localhost:8182/ || exit 1  
CMD ["/build/entrypoint.sh"]  

