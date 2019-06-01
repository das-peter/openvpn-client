FROM python:3-stretch

# Install requirements
RUN apt-get update \
  && apt-get install -q -y python3-dev libdbus-glib-1-dev

# Add chromedriver
RUN apt-get update \
    && apt-get install -q -y libnss3-dev \
    && wget https://chromedriver.storage.googleapis.com/2.41/chromedriver_linux64.zip \
    && unzip chromedriver_linux64.zip \
    && mv chromedriver /usr/bin/chromedriver \
    && chmod +x /usr/bin/chromedriver \
    && rm chromedriver_linux64.zip

# Fetch test suite
RUN wget https://github.com/expressvpn/expressvpn_leak_testing/archive/master.zip \
    && unzip master.zip \
    && mv /expressvpn_leak_testing-* /expressvpn_leak_testing \
    && rm *.zip

# Fixing requirement
RUN ln -s /usr/local/bin/virtualenv /usr/bin/virtualenv

# Init Test-Suite
RUN cd /expressvpn_leak_testing && ./setup_python.sh /test-suite

WORKDIR /test-suite

CMD tail -f /dev/null