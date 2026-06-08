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

- (NOVO) Estatísticas de rede diretamente extraídas para fácil análise e abuse monitoring; VictoriaMetrics para outras estatísticas globais e particulares.
- Outros elementos a designar

# Sistemas Operativos para Target no Control Server e nos Hypervisors.

Os sistemas Linux primariamente suportados são os mesmos para Control Server e Hypervisors:

» AlmaLinux 10.x (preferencial)

» Red Hat Enterprise Linux 10.x 

» Rocky Linux 10.x 

» SUSE Linux Enterprise Server

» OpenSUSE Tumbleweed

» Debian 13. 

Outros sistemas Linux não serão suportados nativamente por não haver razão técnica ou comercial que o justifique.
Sistemas para hypervisor mais antigos, mas da mesma categoria, também não serão suportados: esta ferramenta utiliza exclusivamente nftables e nunca iptables.

Os sistemas Windows primariamente suportados são-no em Control Server (incluindo Server Core) - algo raro no setor - e em Máquinas Virtuais KVM:

» Windows Server 2019

» Windows Server 2022 

» Windows Server 2026

Hypervisors suportarão Hyper-V via KVM (VMs globais sobem virtualizadas em Windows com Enlightenments, base Linux), uma solução que retém em média 100% da performance original, permite maior isolamento, configurações mais fáceis (incluindo possibilidade ampla de SR-IOV) e melhor virtualização. 

O versioning destes OS é estável, possibilitando por si uma estabilidade natural no serviço providenciado ao Cliente.

O sistema está todo ele pensado para, do Control Server aos Hypervisors, ser o mais monolítico e empresarial possível na abordagem.

# Funções Principais

- Aprovisionamento automático de hypervisors e de control server via scripting direto, tal como todos os outros toolings similares, mas com configuração automática de rede (como SolusVM 2)

- Lite Version com páginas carregáveis em texto, sem imagens, acessível de forma muito leve e baseada a gestão de conta em texto, e consola virsh exposta para gestão da VM. Compatível com redes GPRS/EDGE/UMTS+, linhas telefónicas 56K e RDIS, e ligações por satélite pré-Leo/Starlink e similares. Permite gestão de VMs e de conta-cliente quer de forma fixa, em computadores que suportem browsers como Lynx, quer em movimento e até em telemóveis com Symbian S60 ou Blackberry (via Opera Mini), possibilitando uma adaptação ao estilo de vida do Cliente em qualquer lugar.

- Full Version de carregamento rápido, poderosa mas simplificada no display, sem overlays pesados para com o servidor - até 10x mais performance que soluções comerciais de control server/hypervisor baseadas a PHP/Laravel, com ASP.NET Core + Blazor/Razor + Go.

- Cross-platform: 1º control system que permite deployment em Windows Server, Linux e BSD desde que os toolings corretos sejam suportados e estejam instalados.

- Gestão automática de utilizadores e migração in-place, com controlos in-VM e em tempo real

- Interface fácil e acessível até para novatos, mas sem esconder informação essencial para clientes especializados: nova filosofia de interface no client side e no admin side. Compatível com sistemas e ecrãs touch.

- Sistemas automatizados de controlo de parâmetros comerciais com granularidade por plano, utilizador, VM e servidor dedicado, com hierarquia própria.

- Sistemas automatizados de controlo de aspetos técnicos de volumetria de rede, utilização de CPU e utilização de disco.

- Gestão de abuse de CPU, disco e rede de forma totalmente automática e altamente granular.

- Implementação de opções para ballooning (não implementado by default) para situações em que seja necessária uma partilha pontual de páginas inter-VM ou gestão de RAM interservidor por razões comerciais ou técnicas e para garantir estabilidade junto do cliente, com granularidade por VM, por plano e/ou por utilizador

- Suporte nativo a 2FA e atualização de informações, estados e pacotes comerciais em tempo real e <5 segundos, com gestão automática.

- Utilização da figura de Perfis de Hardware para situar pacotes comerciais nos respetivos Perfis de configuração, e aprovisionar automaticamente da forma mais eficaz possível conforme tooling que o requeira no hypervisor system, sem necessidade de atualizações

- Suporte a DHCPv4, DHCPv6, Port Isolation, gestão de NICs, SR-IOV, e configuração automática de redes v4 e v6 sem necessidade de edição de ficheiros.

- Suporte a scripting pré e pós-arranque em estrutura própria simplificada

- Suporte a migrações live e migrações semi-live, quase sem downtime, com retirada e recolocação automática de IPs NAT

- Suporte a figuras de High Availability e Latency-Sensitive em VMs participadas: serviços detidos pelo Cliente em dois ou mais pontos distintos podem ser replicados para failover automático e extremamente fácil de ativar. Ideal para situações em que um serviço simplesmente não pode falhar.

- Opções para sistemas remotos de storage como S3, NFS e SFTP e gestão de backups em tempo real com formato próprio do sistema e encriptação automática

- (NOVO) Introdução de um sistema de two-tiering no backup: "hot backups" em lz4/zstd/gzip customizável, "cold backups" automaticamente convertidos para poupança máxima de recursos pelo Provedor em lzma2. Descompressões são mais rápidas que compressões.

- Inauguração da área de "Observabilidade": um one-stop shop para todos os dados inter-servidores dedicados e Inter-VMs

- Simplificação da área de Hourly Billing para meras comunicações inter-API, gestão virtual por hora e cálculo correto de fundos inspirado em SolusVM 2

- Gestão complementar de clientes para servidores dedicados (via APIs dos principais fabricantes), clientes para semi-dedicados ou carry-over (sistema híbrido) e para containers (sistema de containers a designar).

- (NOVO) Gestão complementar de clientes em formato Reseller, nova categoria de transação, quer por venda direta + mapping do produto C-Servers, quer por venda em website próprio em WHMCS e Blesta com interação in-store com a VM por parte do Cliente, em VPS/VDS e servidores dedicados. Desenvolvimento de API reseller para prepaid e post-paid systems e para comunicação de VMs. Primeiro sistema 360º da indústria com hosting + reselling no mesmo head-control e em módulos-satélite.

- Capacidade de fácil replicação multissistemas para evitar períodos de downtime de plataforma junto do Cliente, em todas as frentes.

# Estado atual
Fase 0, 1, 2, 3, 4, 5 e 6 concluídas; Refinação de elementos de comunicação e ponderação de outros fatores em curso. Fase 7 em curso. Hardening em curso.
Encontra-se, à data de 08-06-2026, em Technical Beta.

Total de fases de desenvolvimento previstas: 9
