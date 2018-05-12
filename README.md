# Ansible Role: Logstash

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-logstash.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-logstash)

An Ansible Role that installs Logstash on RedHat/CentOS Debian/Ubuntu.

Note that this role installs a syslog grok pattern by default; if you want to add more filters, please add them inside the `/etc/logstash/conf.d/` directory. As an example, you could create a file named `13-myapp.conf` with the appropriate grok filter and restart logstash to start using it. Test your grok regex using the [Grok Debugger](http://grokdebug.herokuapp.com/).

## Requirements

Though other methods are possible, this role is made to work with Elasticsearch as a backend for storing log messages.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    logstash_listen_port_beats: 5044

The port over which Logstash will listen for beats.

    logstash_elasticsearch_hosts:
      - http://localhost:9200


## Other Notes

If you are seeing high CPU usage from one of the `logstash` processes, and you're using Logstash along with another application running on port 80 on a platform like Ubuntu with upstart, the `logstash-web` process may be stuck in a loop trying to start on port 80, failing, and trying to start again, due to the `restart` flag being present in `/etc/init/logstash-web.conf`. To avoid this problem, either change that line to add a `limit` to the respawn statement, or set the `logstash-web` service to `enabled=no` in your playbook, e.g.:

    - name: Ensure logstash-web process is stopped and disabled.
      service: name=logstash-web state=stopped enabled=no

## Example Playbook



## License

MIT / BSD


