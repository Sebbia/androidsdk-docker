FROM sebbia/androidsdk-docker:30.0.3

RUN git clone https://github.com/flutter/flutter.git /flutter
ENV PATH "$PATH:/flutter/bin"
RUN flutter upgrade
RUN flutter doctor