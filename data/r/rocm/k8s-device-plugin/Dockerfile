# Copyright 2018 Advanced Micro Devices, Inc. All rights reserved.  
#  
# Licensed under the Apache License, Version 2.0 (the "License");  
# you may not use this file except in compliance with the License.  
# You may obtain a copy of the License at  
#  
# http://www.apache.org/licenses/LICENSE-2.0  
#  
# Unless required by applicable law or agreed to in writing, software  
# distributed under the License is distributed on an "AS IS" BASIS,  
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
# See the License for the specific language governing permissions and  
# limitations under the License.  
FROM golang:1.9.5-alpine3.7  
RUN mkdir -p /go/src/github.com/RadeonOpenCompute/k8s-device-plugin  
ADD . /go/src/github.com/RadeonOpenCompute/k8s-device-plugin  
RUN go install github.com/RadeonOpenCompute/k8s-device-plugin  
  
FROM alpine:3.7  
MAINTAINER Kenny Ho <Kenny.Ho@amd.com>  
RUN apk --no-cache add ca-certificates  
WORKDIR /root/  
COPY \--from=0 /go/bin/k8s-device-plugin .  
CMD ["./k8s-device-plugin", "-logtostderr=true", "-stderrthreshold=INFO",
"-v=5"]  

