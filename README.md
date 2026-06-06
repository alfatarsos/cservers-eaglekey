# C-Servers EagleKey
A turn-key solution for virtualization systems with a simplifying approach

------------description proceeds below in Portuguese, an English description will be available soon------------
# O que é
Plataforma de virtualização / IaaS auto-alojada, no modelo duplo control server ↔ hypervisors, com vasta riqueza de funcionalidades mas com forte procura de simplificação de aspetos técnicos, e uma interface intuitiva e bonita, para o Cliente.

Inspira-se no VirtFusion mas parte para soluções completamente diferentes, numa lógica clean-room em estreito cumprimento dos termos e condições do software. Pode ainda utilizar como inspiração outras bases de referência com as quais o autor tenha tido contacto (ex: Proxmox, SolusVM 2) para determinadas funções. 

Implementa, ainda, novas funcionalidades de qualidade de vida para o Cliente, como as aplicáveis à gestão automática de NAT e gestão de painel.

# Porquê o nome EagleKey?

Porque num mercado de hosting virtual ou dedicado, ter uma plataforma única detida pela própria empresa que vende o serviço, mutável e adaptável às necessidades existentes e futuras, é um fator chave (key) de diferenciação, e permite uma perspetiva de serviço amplamente abrangente - tal como uma águia (Eagle).

E para ser honesto, porque foi o melhor nome que ocorreu ao autor no espaço de 5 minutos que não pertencia a qualquer outra marca no setor tecnológico.

# Esta nova plataforma vai criar disrupção a quem tem VMs, como ocorre em migrações entre produtos de hypervisor (e.g. SolusVM » VirtFusion, Proxmox » Virtualizor)?

Não. A plataforma será um drop-in replacement na estrutura (coroa) imediatamente exterior aos servidores abrangidos, que continuarão a correr como normalmente, e permitirá quer um clean-slate approach (implementação do zero), quer um in-place conversion approach (potencialmente introduzindo pequenas breaking changes que não afetam o acesso às VMs, mas poderão até melhorar a abordagem). 

Utiliza QEMU/KVM e os servidores correm em QEMU/KVM, que é open-source e utilizável por todos; utiliza tecnologias de networking como libvirt, MacVTap, OpenVSwitch, que são open-source; opera no user-space e kernel-space de Linux, que é open-source. Nada do que é utilizado pelos produtos comerciais são elementos patenteáveis, com a exceção da recipe (própria), grafismos e forma de implementação (o chamado IP). Como tal, os utilizadores podem continuar como normalmente com os seus serviços. 

# Princípios de design
1.	Simples — pouca cerimónia, fácil de raciocinar e operar.
2.	Rápido — baixa latência, baixo consumo de recursos.
3.	Bonito — UI moderna e cuidada (admin + cliente).
4.	Replicável ao infinito — deploy trivial, idempotente, num e noutro lado.
5.	Fiável — operações seguras, idempotentes e auditáveis sobre as VMs.

# Stack (decidida — modelo híbrido)
·	Agente (cada host KVM): Go — binário único, libvirt/nftables nativos.

·	Control plane: .NET (ASP.NET Core + Blazor Server) — UI rica e tempo real.

·	Base de dados: PostgreSQL (importação one-time do MariaDB atual).

·	Contrato control↔agente: HTTP/JSON + TLS, JWT RS256 curto, spec OpenAPI.

·	Cache/fila/realtime: Redis/Valkey. Console: WebSocket → noVNC.

- Outros elementos a designar

# Sistemas Operativos para Target no Control Server e nos Hypervisors.

AlmaLinux 10 (preferencial) e Debian 13. O versioning destes OS é estável, possibilitando por si uma estabilidade natural no serviço providenciado ao Cliente, ao contrário do que acontece com sistemas como Ubuntu Server, Fedora Server, CentOS Stream e Arch Linux (entre outros), que podem introduzir bugs e indisponibilidades num lado ou noutro. 

O sistema está todo ele pensado para, do Control Server aos Hypervisors, ser o mais monolítico e empresarial possível na abordagem.

Sistemas potencialmente compatíveis: outros RHEL-based com o kernel fixo pela Red Hat (Rocky Linux 10, Oracle Linux 10 na variante non-UEK) e openSUSE Leap / SUSE Linux Enterprise Server.

Outros sistemas Linux não serão suportados nativamente por não haver razão técnica ou comercial que o justifique.

Está a ser observada, a título complementar: a viabilidade potencial de operação em Windows com Windows Server Core no control server e/ou nos hypervisors (e utilização complementar de Hyper-V, sobretudo para VMs Windows-based), e com BSD no control server + bhyve nos hypervisors. Também Xen está a ser analisado.

# Estado atual
Fase 0 concluída + Fase 1 em curso.

·	Fase 0: control (.NET) ↔ agente (Go) por JWT RS256, /v1/ping ponta-a-ponta.

·	Fase 1 (parcial): gerador de XML de domínio libvirt (q35/RAW/virtio/VNC/guest-agent) + ligação ao libvirt (/v1/host); UI admin + cliente navegável.

Total de fases de desenvolvimento previstas: 9
