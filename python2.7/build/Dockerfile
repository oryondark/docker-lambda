FROM lambci/lambda-base:build

ENV AWS_EXECUTION_ENV=AWS_Lambda_python2.7

RUN rm -rf /var/runtime /var/lang && \
  curl https://lambci.s3.amazonaws.com/fs/python2.7.tgz | tar -zx -C /

# Add these as a separate layer as they get updated frequently
RUN curl --silent --show-error --retry 5 https://bootstrap.pypa.io/get-pip.py | python && \
  pip install -U 'virtualenv>=16.0.0,<20.0.0' pipenv wheel --no-cache-dir && \
  curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/1.0.9/get-poetry.py | POETRY_VERSION=1.0.9 python && \
  pip install -U awscli boto3 aws-sam-cli==0.22.0 aws-lambda-builders==0.4.0 --no-cache-dir

ENV PATH=/root/.poetry/bin:$PATH
