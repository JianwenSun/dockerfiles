# build stage  
FROM golang:1.10.2-alpine3.7 AS build-env  
RUN apk --no-cache add git  
RUN go get github.com/pstuifzand/ekster/cmd/eksterd  
  
# final stage  
FROM alpine  
RUN apk --no-cache add ca-certificates  
RUN ["mkdir", "-p", "/opt/micropub"]  
WORKDIR /opt/micropub  
EXPOSE 80  
COPY \--from=build-env /go/bin/eksterd /app/  
ENTRYPOINT ["/app/eksterd"]  

