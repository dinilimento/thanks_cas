FROM alpine:latest
ARG TERRAFORM_VERSION=0.11.5
ARG PACKER_VERSION=1.2.1
ARG ANSIBLE_VERSION=2.3.1.0
ARG ANSIBLE_LINT_VERSION=3.4.13
ARG TERRAFORM_PROVIDER_ARCHIVE_VERSION=1.0.3
ARG TERRAFORM_PROVIDER_AWS_VERSION=1.13.0
ARG TERRAFORM_PROVIDER_TEMPLATE_VERSION=1.0.0
ARG TERRAFORM_PROVIDER_TERRAFORM_VERSION=1.0.2
ARG PYWINRM_VERSION=0.2.2
RUN apk add --no-cache python2 make openssh-client git zip curl coreutils sed libssl1.0 bash json-glib-dev \
    bind-tools jq
RUN apk add --no-cache --virtual build-dependencies python2-dev gcc musl-dev libffi-dev openssl-dev && \
    python2 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools && \
    pip install boto3 && \
    pip install dnspython && \
    pip install awscli && \
    pip install "ansible==${ANSIBLE_VERSION}" "pywinrm>=${PYWINRM_VERSION}" && \
    pip install "ansible-lint==${ANSIBLE_LINT_VERSION}" && \
    rm -r /root/.cache && \
    apk del build-dependencies
RUN wget https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip && \
    unzip packer_${PACKER_VERSION}_linux_amd64.zip && \
    rm packer_${PACKER_VERSION}_linux_amd64.zip && \
    mv packer /usr/local/bin/packer
RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    mv terraform /usr/local/bin/terraform && \
  mkdir /usr/lib/custom-terraform-plugins
RUN wget https://releases.hashicorp.com/terraform-provider-archive/${TERRAFORM_PROVIDER_ARCHIVE_VERSION}/terraform-provider-archive_${TERRAFORM_PROVIDER_ARCHIVE_VERSION}_linux_amd64.zip && \
    unzip terraform-provider-archive_${TERRAFORM_PROVIDER_ARCHIVE_VERSION}_linux_amd64.zip && \
    rm terraform-provider-archive_${TERRAFORM_PROVIDER_ARCHIVE_VERSION}_linux_amd64.zip && \
    mv terraform-provider-archive* /usr/lib/custom-terraform-plugins/terraform-provider-archive
RUN wget https://releases.hashicorp.com/terraform-provider-aws/${TERRAFORM_PROVIDER_AWS_VERSION}/terraform-provider-aws_${TERRAFORM_PROVIDER_AWS_VERSION}_linux_amd64.zip && \
    unzip terraform-provider-aws_${TERRAFORM_PROVIDER_AWS_VERSION}_linux_amd64.zip && \
    rm terraform-provider-aws_${TERRAFORM_PROVIDER_AWS_VERSION}_linux_amd64.zip && \
    mv terraform-provider-aws* /usr/lib/custom-terraform-plugins/terraform-provider-aws
RUN wget https://releases.hashicorp.com/terraform-provider-template/${TERRAFORM_PROVIDER_TEMPLATE_VERSION}/terraform-provider-template_${TERRAFORM_PROVIDER_TEMPLATE_VERSION}_linux_amd64.zip && \
    unzip terraform-provider-template_${TERRAFORM_PROVIDER_TEMPLATE_VERSION}_linux_amd64.zip && \
    rm terraform-provider-template_${TERRAFORM_PROVIDER_TEMPLATE_VERSION}_linux_amd64.zip && \
    mv terraform-provider-template* /usr/lib/custom-terraform-plugins/terraform-provider-template
RUN wget https://releases.hashicorp.com/terraform-provider-terraform/${TERRAFORM_PROVIDER_TERRAFORM_VERSION}/terraform-provider-terraform_${TERRAFORM_PROVIDER_TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform-provider-terraform_${TERRAFORM_PROVIDER_TERRAFORM_VERSION}_linux_amd64.zip && \
    rm terraform-provider-terraform_${TERRAFORM_PROVIDER_TERRAFORM_VERSION}_linux_amd64.zip && \
    mv terraform-provider-terraform* /usr/lib/custom-terraform-plugins/terraform-provider-terraform
CMD ["/bin/sh"]
