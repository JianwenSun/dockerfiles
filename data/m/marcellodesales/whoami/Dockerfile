FROM golang:alpine3.6 AS binary  
ADD . /app  
WORKDIR /app  
RUN go build -o http  
  
FROM alpine:3.6  
WORKDIR /app  
ENV PORT 8000  
EXPOSE 8000  
COPY \--from=binary /app/http /app  
ARG VERSION  
RUN echo $VERSION > /app/version  
ARG LABEL  
RUN echo $LABEL > /app/label  
  
CMD ["/app/http"]  

