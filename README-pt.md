<p align="center">
<img width="199" height="200" alt="logoeaglekey-jpg" src="https://github.com/user-attachments/assets/1dd4ff58-3b30-4885-bb00-7419d3d85e23" />
</p>

# C-Servers EagleKey
Uma solução turn-key para sistemas de virtualização com uma abordagem simplificada

# O que é

Uma plataforma de virtualização/IaaS auto-hospedada, baseada num modelo de servidor de controlo duplo ↔ hipervisor, com uma vasta gama de funcionalidades, mas com um forte foco na simplificação dos aspetos técnicos e uma interface intuitiva e elegante para o cliente.

<p align="center">
<img width="840" height="525" alt="eg8" src="https://github.com/user-attachments/assets/2fc54c81-4162-4fdb-97c8-d171d681807a" />
</p>

<p align="center">
<img width="840" height="525" alt="eg5" src="https://github.com/user-attachments/assets/d30ce6e4-76f0-4190-a15b-5f732dc69db8" />
</p>

Inspira-se no VirtFusion, mas adota soluções completamente diferentes, com uma lógica totalmente nova e em estrita conformidade com os termos e condições do software. Outras fontes de inspiração também existem (por exemplo, Proxmox, SolusVM 2) para determinadas funções.

Implementa ainda novas funcionalidades que melhoram a experiência do utilizador, como as aplicáveis ​​à gestão automática de NAT e à gestão de painéis de controlo.

<p align="center">
<img width="840" height="525" alt="eg6" src="https://github.com/user-attachments/assets/be2aa2dd-43ae-4997-aa93-bcd888c4e04a" />
</p>

<p align="center">
<img width="840" height="525" alt="eg4" src="https://github.com/user-attachments/assets/99489a67-4c86-4d3d-b71f-f2fbd5cd2db6" />
</p>

# Porquê o nome EagleKey?

Porque, num mercado de alojamento virtual ou dedicado, ter uma plataforma única, própria da empresa que comercializa o serviço, mutável e adaptável às necessidades presentes e futuras, é um diferencial fundamental e permite uma perspetiva de serviço abrangente – tal como uma águia.

E, para ser sincero, porque foi o melhor nome que me ocorreu em 5 minutos e que não pertencia a mais nenhuma marca do setor tecnológico.

# Esta nova plataforma causará transtorno a quem utiliza VMs, como acontece nas migrações entre hipervisores?

Não. A plataforma é uma substituição direta na estrutura (coroa) imediatamente externa aos servidores abrangidos, que continuarão a funcionar normalmente, permitindo tanto uma implementação de raiz como uma conversão no local com apenas 15 segundos de inatividade.

Utiliza QEMU/KVM, e os servidores correm em QEMU/KVM, que é open source e acessível a todos; Utiliza tecnologias de rede como a libvirt e o MacVTap, que são de código aberto; opera no espaço do utilizador e no espaço do kernel do Linux, que também são de código aberto. Nada do que é utilizado em produtos comerciais é patenteável, exceto a receita (proprietária), os gráficos e o método de implementação (a chamada propriedade intelectual). Nenhum destes elementos é aqui utilizado, como se pode observar nas imagens.

# Princípios de Design
1. Simples — pouca complexidade, fácil de compreender e de operar.

2.º Rápido — baixa latência, baixo consumo de recursos.

3.º Bonito — interface de utilizador moderna e bem concebida (administrador + cliente).

4.º Infinitamente replicável — implantação trivial e idempotente em ambos os lados.

5.º Fiável — operações seguras, idempotentes e auditáveis ​​em máquinas virtuais.

# Pilha (definida — modelo híbrido)
• Agente (cada host KVM): Go — um único binário em Go, libvirt/nftables nativo e comunicação com o plano de controlo.

• Plano de controlo: .NET (ASP.NET Core + Blazor Server) — interface de utilizador rico e em tempo real; Kestrel e Nginx. Desempenho até 10 vezes superior a soluções similares baseadas em PHP, com manutenção contínua garantida em ambas as plataformas: Go e .NET mantêm a compatibilidade e a lógica de código entre versões durante muitos anos.

• Base de dados: PostgreSQL.

• Cache/fila/tempo real: Redis/Valkey. Consola: WebSocket → noVNC, Consola Serial.

- VictoriaMetrics para outras estatísticas globais e privadas e verificação geral de disponibilidade, pública e privada.

# Sistemas Operativos Alvo

Os sistemas Linux suportados são os mesmos para o Servidor de Controlo e para os Hipervisores:

» AlmaLinux 10. x (preferencial)

» Red Hat Enterprise Linux 10.x

» Rocky Linux 10. x

» Oracle Linux 10. x

» Debian 13

» outros a referenciar

Os sistemas de hipervisor mais antigos ou os sistemas que não implementem nftables por defeito não serão suportados: esta ferramenta utiliza exclusivamente nftables e nunca iptables.

Os principais sistemas operativos Windows suportados são o Servidor de Controlo (incluindo o Server Core) – uma raridade no setor – e as Máquinas Virtuais KVM:

» Windows Server 2019

» Windows Server 2022

» Windows Server 2026

Os hipervisores serão compatíveis com o Hyper-V via KVM (VMs globais executadas virtualizadas no Windows com Enlightenments), uma solução que mantém, em média, 99% do desempenho original, permite um maior isolamento, configurações mais fáceis (incluindo amplas possibilidades de SR-IOV) e uma melhor virtualização.

Todo o sistema, desde o Servidor de Controlo aos Hipervisores, foi concebido para ser o mais monolítico e amigável possível para ambientes empresariais. O versionamento destes sistemas operativos é estável, garantindo estabilidade inerente ao serviço prestado ao cliente.

# Algumas das principais funções

- Provisionamento automático de hipervisores e servidor de controlo através de script direto, como noutras ferramentas semelhantes, mas com configuração automática de rede (como o SolusVM 2) e uma ferramenta de script manual como alternativa.

- Versão Lite com páginas de texto carregáveis, sem imagens, muito leve e com gestão de contas baseada em texto, incluindo consola. Compatível com redes GPRS/EDGE/UMTS+, linhas telefónicas 56K e RDIS, e ligações satélite pré-Leo/Starlink e similares. Permite a gestão de contas de VM e de clientes tanto num local fixo, em computadores que suportem browsers como o Lynx, como em movimento, incluindo em telemóveis com Symbian S60 ou Blackberry (via Opera Mini), possibilitando a adaptação ao estilo de vida do cliente em qualquer lugar.

- Desempenho até 10 vezes superior às soluções comerciais de servidor/hipervisor de controlo baseadas em PHP/Laravel, com ASP.NET Core + Blazor/Razor + Go.

- Gestão automática de utilizadores e migração in-place, com controlos em tempo real e na própria VM.

- Interface fácil e acessível, mesmo para principiantes, mas sem ocultar informação essencial para clientes especializados: nova filosofia de interface tanto do lado do cliente como do lado do administrador. Compatível com ecrãs e sistemas sensíveis ao toque.

- - Sistemas automatizados para controlo de parâmetros de negócio com granularidade por plano, utilizador, máquina virtual e servidor dedicado, com hierarquia própria; e para controlo de aspetos técnicos como o volume de rede, utilização de CPU, utilização de RAM e utilização de disco, automatizados.

ically.

- Suporte nativo para autenticação de dois fatores (2FA) e atualizações em tempo real e a cada 60 segundos de informação, estado e pacotes comerciais, com gestão automática.

- Utilização de perfis de hardware para posicionar os pacotes comerciais nos seus respetivos perfis de configuração e provisioná-los automaticamente da forma mais eficiente possível, de acordo com as ferramentas exigidas pelo sistema hipervisor, sem necessidade de atualizações. Pré-compatível com a versão mais recente do QEMU.

- Suporte para DHCPv4, DHCPv6, isolamento de portas, gestão de NIC, SR-IOV e configuração automática de redes v4 e v6 sem necessidade de editar ficheiros; scripts de pré e pós-inicialização são compatíveis numa estrutura simplificada em Provisionadores. Perfilador de rede para aprovisionamento automático de soluções VPS/Servidor de interface dupla e aprovisionamento/alterações automáticas nas regras NAT e HAProxy, incluindo um novo botão, "Limpar NAT", quando um cliente fica sem acesso NAT devido ao conntrack manter uma ligação ativa.

- - Suporte para migrações ao vivo e semi-ao vivo, com tempo de inatividade praticamente nulo, com remoção e substituição automática de IPs NAT.

- Suporte para características de alta disponibilidade e sensíveis à latência em VMs controladas: os serviços mantidos pelo Cliente em dois ou mais locais distintos podem ser replicados para failover automático e são extremamente fáceis de ativar. Ideal para situações em que um serviço simplesmente não pode falhar.

- Opções para sistemas de armazenamento remoto como S3, NFS, SSH, rclone e SFTP, e gestão de cópias de segurança em tempo real com formato específico do sistema e encriptação automática. Introdução de um sistema de cópias de segurança de duas camadas: cópias de segurança "a quente" personalizáveis ​​em lz4/zstd/gzip e cópias de segurança "a frio" convertidas automaticamente para máxima poupança de recursos pelo Fornecedor em lzma2. A descompressão é mais rápida que a compressão.

- Lançamento da área "Observabilidade": um ponto único de acesso para todos os dados entre servidores dedicados e entre VMs.

- - Simplificação da área de faturação por hora para comunicação inter-API simplificada, gestão virtual de horas e cálculo preciso de fundos, inspirado no SolusVM 2.

- Gestão complementar de clientes para servidores dedicados (via APIs dos principais fabricantes), clientes para servidores semi-dedicados ou com possibilidade de transferência de tempo (sistema híbrido) e para contentores (sistema de contentores a atribuir).

- Gestão complementar de clientes no formato Revendedor, uma nova categoria de transação, seja através de vendas diretas + mapeamento do produto C-Servers, ou através de vendas num site dedicado no WHMCS e Blesta com interação direta com a VM por parte do Cliente, em servidores VPS/VDS e dedicados. Desenvolvimento de uma API de revenda para sistemas pré-pagos e pós-pagos e para comunicação com VMs. O primeiro sistema 360º do setor com alojamento + revenda para servidores virtuais e dedicados.

- Página de tempo de atividade diretamente na plataforma, sem necessidade de utilizar uma solução separada, interna ou externamente (para clientes).

- - Traduzido para 8 idiomas: inglês, português (Brasil), português (Portugal), espanhol, francês, alemão, chinês e árabe.

- Suporte completo para anúncios BGP, trânsito IP e tunelamento em servidores VPS e dedicados.

- Medidas de segurança para o cliente e fácil integração.

- Facilmente replicável em múltiplos sistemas para evitar o tempo de inatividade da plataforma para o cliente, em todas as frentes.

# Estado atual
Fases 0, 1, 2, 3, 4, 5, 6 e 7 concluídas; refinamento dos elementos de comunicação e consideração de outros fatores em curso. Fase 8 em curso.

A 12 de junho de 2026, está na versão Beta 3 (próximos níveis de estado a obter: Beta 4, RC1, RC2, RC3+).

Total de fases de desenvolvimento planeadas: 10
