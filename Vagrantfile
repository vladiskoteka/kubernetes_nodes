IMAGE_NAME = "bento/ubuntu-20.04"
N = 2
Vagrant.configure("2") do |config|
    #config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2024
        v.cpus = 1
    end


    (1..N).each do |i|
        config.vm.define "node#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "10.100.10.#{i + 10}"
            node.vm.hostname = "node#{i}"
            node.vm.provision "ansible" do |ansible|
               ansible.playbook = "kubernetes-setup/node-playbook_latest.yml"
               ansible.extra_vars = {
                   node_ip: "10.100.10.#{i + 10}",
                   kubernetes_token: "kubeadm join 10.100.10.1:6443 --token 4nbsse.r6ykw1g9xfmug7uu     --discovery-token-ca-cert-hash sha256:978c994f389e2f38395877adc7334c9d82379c7d0fe97aec3470d9628601af96"
               }
            end
        end
    end
end

