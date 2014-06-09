# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
PROXY_VAGRANTFILE_PATH  = "./Vagrantfile.proxy"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "icecast" do |v|
    v.vm.provider "docker" do |d|
      d.name  = "icecast"
      d.image = "moul/icecast"
      d.ports = ["8000:8000"]

      # Assign the container the hostname "icecast"
      d.create_args = ["-h", "icecast"]

      d.env = {
        SOURCE_PASSWORD: 'hackme',
        # ADMIN_PASSWORD:  'password',
        # PASSWORD:        'hackme',
        # RELAY_PASSWORD:  'password'
      }

      d.vagrant_vagrantfile = PROXY_VAGRANTFILE_PATH
    end
  end

  config.vm.define "mpd" do |v|
    v.vm.provider "docker" do |d|

      d.build_dir = "./mpd"
      d.ports     = ["6600:6600"]

      # Mount a read-only volume for media.
      d.volumes = ["/vagrant/music:/var/lib/mpd/music:ro"]
      d.link("icecast:icecast")

      d.vagrant_vagrantfile = PROXY_VAGRANTFILE_PATH
    end
  end
end
