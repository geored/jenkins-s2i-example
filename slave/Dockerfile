# The FROM will be replaced when building in OpenShift
FROM registry.redhat.io/rhel7/rhel

MAINTAINER Siamak Sadeghianfar <ssadeghi@redhat.com>

# Install headless Java
USER root
RUN yum clean all
RUN yum-config-manager --disable rhel* 1>/dev/null
RUN yum-config-manager --enable rhel-7-server-rpms
RUN yum-config-manager --enable rhel-7-server-ose-3.2-rpms
RUN export INSTALL_PKGS="nss_wrapper java-1.8.0-openjdk-headlessjava-1.8.0-openjdk-devel nss_wrapper gettext tar git"
# RUN yum clean all
RUN yum install -y --setopt=tsflags=nodocs install $INSTALL_PKGS
RUN rpm -V $INSTALL_PKGS
# RUN yum clean all
RUN mkdir -p /var/lib/jenkins
RUN chown -R 1001:0 /var/lib/jenkins
RUN chmod -R g+w /var/lib/jenkins

# Copy the entrypoint
COPY configuration/* /var/lib/jenkins/
USER 1001

# Run the JNLP client by default
# To use swarm client, specify "/var/lib/jenkins/run-swarm-client" as Command
ENTRYPOINT ["/var/lib/jenkins/run-jnlp-client"]
