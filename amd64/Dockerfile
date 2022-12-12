FROM amazonlinux:latest

LABEL maintainer="m4rkus@engineers4cloud" description="docker buid image for CI-Pipelines" version="latest"

ENV PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/opt/aws/bin:/root/bin"
ENV TZ="etc/localtime"
RUN yum update -y \
&& yum install -y unzip jq less groff wget \
&& amazon-linux-extras install docker \
&& yum clean all \
&& rm -rf /var/cache/yum \
&& curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
&& unzip -q awscliv2.zip \
&& ./aws/install \
&& rm -rf awscliv2.zip \
aws \
/usr/local/aws-cli/v2/*/dist/aws_completer \
/usr/local/aws-cli/v2/*/dist/awscli/data/ac.index \
/usr/local/aws-cli/v2/*/dist/awscli/examples
RUN BUILDX_VERSION=$(curl -sL "https://api.github.com/repos/docker/buildx/releases/latest" | jq -r ".tag_name" | cut -c2-10) \
&& echo $BUILDX_VERSION \
&& wget -q "https://github.com/docker/buildx/releases/download/v${BUILDX_VERSION}/buildx-v${BUILDX_VERSION}.linux-amd64" \
&& ls -l
