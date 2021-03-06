drf-to-s3
=========

Interface for direct upload to S3 using the [POST API][].

Designed for use with the [Fine Uploader][] and
[Django REST Framework][].

This service has a few essential responsibilities:

 1. Sign [policy documents][]
 2. Provide an empty response to use as a success action redirect
    with old browsers (IE 9 and Android 2.3.x) which do not support
    the File API, instead using a dynamically generated iframe
 3. Provide an upload-complete callback

See this [Fine Uploader blog post][] for a long explanation of
these responsibilities.

Status
------

This project is functional pre-alpha. Most significantly it needs
some documentation.

[![Build Status](https://travis-ci.org/bodylabs/drf-to-s3.png?branch=master)](https://travis-ci.org/bodylabs/drf-to-s3)

Integrating into your project
-----------------------------

1. `pip install drf_to_s3`
2. ...

Development
-----------

    npm install -g grunt-cli
    brew update
    brew install chromedriver
    brew tap phinze/cask
    brew install brew-cask
    brew cask install pandoc
    virtualenv venv
    source venv/bin/activate
    pip install -r requirements_dev.txt

### Running tests ###

    foreman run drf_to_s3/runtests/runtests.py

### Running tests including S3 ###

Create .env with AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY

    foreman run drf_to_s3/runtests/runtests.py

### Running Fine Uploader integration tests ###

1. Create .env with AWS_UPLOAD_BUCKET, AWS_ACCESS_KEY_ID, and AWS_SECRET_ACCESS_KEY
2. Choose a version to test and install it:

    ./fine-uploader-build.sh version

3. foreman run drf_to_s3/runtests/runtests.py integration

To run them on Sauce Labs:

1. Create a Sauce Labs account
2. Set SAUCE_USERNAME and SAUCE_ACCESS_KEY in .env
3. Install [Sauce Connect][]
4. foreman run sh -c 'java -jar ~/code/Sauce-Connect-latest/Sauce-Connect.jar $SAUCE_USERNAME $SAUCE_ACCESS_KEY'
4. WITH_SAUCE=1 foreman run drf_to_s3/runtests/runtests.py integration

[Django REST Framework]: http://django-rest-framework.org/
[Fine Uploader]: http://fineuploader.com/
[POST API]: http://docs.aws.amazon.com/AmazonS3/latest/dev/HTTPPOSTForms.html
[policy documents]: http://docs.aws.amazon.com/AmazonS3/latest/dev/HTTPPOSTForms.html#HTTPPOSTConstructPolicy
[Fine Uploader blog post]: http://blog.fineuploader.com/2013/08/16/fine-uploader-s3-upload-directly-to-amazon-s3-from-your-browser/
[Sauce Connect]: http://saucelabs.com/downloads/Sauce-Connect-latest.zip
