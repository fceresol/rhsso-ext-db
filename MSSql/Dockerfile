FROM registry.redhat.io/rh-sso-7/sso74-openshift-rhel8:7.4

LABEL maintainer="Filippo Ceresoli - RedHat Consulting filippo.ceresoli@redhat.com"

COPY /extensions /extensions

# Prepare for configuration
ENV DEFAULT_LAUNCH $JBOSS_HOME/bin/openshift-launch.sh
ENV DEFAULT_LAUNCH_NOSTART $JBOSS_HOME/bin/openshift-launch-nostart.sh
RUN cp $DEFAULT_LAUNCH $DEFAULT_LAUNCH_NOSTART
RUN sed -i '/^.*standalone.sh/s/^/echo/' $DEFAULT_LAUNCH_NOSTART
RUN sed -i '/^.*wait/s/^/echo/' $DEFAULT_LAUNCH_NOSTART
RUN $DEFAULT_LAUNCH_NOSTART

# Configure
RUN $JBOSS_HOME/bin/jboss-cli.sh --file=/extensions/actions.cli
RUN $DEFAULT_LAUNCH
