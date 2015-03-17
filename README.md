# Dynatrace-Java-Agent-Ansible

An [Ansible](http://www.ansible.com) role for automated deployments of the [Dynatrace](http://www.bit.ly/dttrial) Java Agent.

This role makes the Java Agent available to a Java Virtual Machine by injecting an appropriate *-agentpath* option into an environment variable, e.g. ```JAVA_OPTS```, inside a file (typically an executable script). It is assumed that this script either executes the Java process directly or is sourced by another script before the Java process gets executed. *Please note that this role might need some tweaking to fit your particular use-case.*

**Note**: You have to restart your application after placing the agent.

**Note**: Currently, we support only Linux hosts, support for installing Windows hosts is in the making.

## Example

We are given a file ```run-foo.sh``` that executes the *main* method in class *Foo*:

```
java Foo
```

By executing this role we change the file's contents to come up with something like this:

```
export JAVA_OPTS="$JAVA_OPTS -agentpath:/opt/dynatrace/agent/lib64/libdtagent.so=name=foo-java-agent,collector=localhost:9998"
java Foo
```

## Download

The role is available via:

- [Ansible Galaxy](https://galaxy.ansible.com/list#/roles/2653)
- [GitHub](https://github.com/Dynatrace/Dynatrace-Java-Agent-Ansible)

## Requirements

This roles requires an installation of the Dynatrace Agents package, which is provided by the following roles:

- [Dynatrace-Agents](https://galaxy.ansible.com/list#/roles/2620)
- [Dynatrace-Server](https://galaxy.ansible.com/list#/roles/2623)

## Role Variables

As defined in ```defaults/main.yml```:

| Name                                      | Default                                  | Description |
|-------------------------------------------|------------------------------------------|-------------|
| *dynatrace_java_agent_env_var_name*       | JAVA_OPTS                                | The name of the environment variable to be used for Agent injection. |
| *dynatrace_java_agent_env_var_file_name*  |                                          | The name of the file to be modified. |
| *dynatrace_java_agent_name*               | java-agent                               | The name of the Agent as it appears in Dynatrace. |
| *dynatrace_java_agent_collector_hostname* | localhost                                | The location of the collector the Agent shall connect to. |
| *dynatrace_java_agent_collector_port*     | 9998                                     | The port on the collector the Agent shall connect to. |
| *dynatrace_java_agent_linux_agent_path*   | /opt/dynatrace/agent/lib64/libdtagent.so | The path to the Agent libary. |
| *dynatrace_java_agent_state*              | present                                  | Whether the Agent shall be ```present``` or ```absent```. |

## Example Playbook

	- hosts: all
	  roles:
	    - role: dynatrace.Dynatrace-Java-Agent
	      dynatrace_java_agent_env_var_file_name: /usr/bin/run-foo.sh

## Additional Resources

- [Slide Deck: Automated Deployments](http://slideshare.net/MartinEtmajer/automated-deployments-slide-share)
- [Slide Deck: Introduction to Automated Deployments with Ansible](http://www.slideshare.net/MartinEtmajer/introduction-to-automated-deployments-with-ansible)
- [Tutorials: Automated Deployments with Dynatrace and Ansible](https://community.compuwareapm.com/community/display/COE/Tutorials+on+Automated+Deployments#TutorialsonAutomatedDeployments-ansible)

## Questions?

Feel free to post your questions on the Dynatrace Community's [Continuous Delivery Forum](https://community.dynatrace.com/community/pages/viewpage.action?pageId=46628921).

## License

Licensed under the MIT License. See the LICENSE file for details.
[![analytics](https://www.google-analytics.com/collect?v=1&t=pageview&_s=1&dl=https%3A%2F%2Fgithub.com%2FdynaTrace&dp=%2FDynatrace-Java-Agent-Ansible&dt=Dynatrace-Java-Agent-Ansible&_u=Dynatrace~&cid=github.com%2FdynaTrace&tid=UA-54510554-5&aip=1)]()