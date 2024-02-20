FROM jenkins/jenkins:lts
# if we want to install via apt
USER root

# Install your required plugins here
RUN jenkins-plugin-cli --plugins "job-dsl basic-branch-build-strategies"

# drop back to the regular jenkins user - good practice
USER jenkins

# Copy the JCasC configuration YAML file into the container
COPY --chown=jenkins:jenkins jenkins.yaml /var/jenkins_home/casc_configs/jenkins.yaml

# Tell Jenkins to use JCasC configuration
ENV CASC_JENKINS_CONFIG /var/jenkins_home/casc_configs/jenkins.yaml

# Run the Jenkins service
CMD ["jenkins", "--httpPort=8080", "--cgi"]
