# Como Instalar o Servidor Web Apache no CentOS 7
*Neste guia, você instalará um servidor web Apache com virtual hosts em seu servidor CentOS 7.*

# Passo 1 — Instalando o Apache

O Apache está disponível nos repositórios de software padrão do CentOS, o que significa que você pode instalá-lo com o gerenciador de pacotes yum.

Agindo como o usuário não-root, com privilégios sudo configurado nos pré-requisitos, atualize o índice de pacotes local httpd do Apache para refletir as alterações mais recentes do upstream:

`sudo yum update -y`

Depois que os pacotes forem atualizados, instale o pacote Apache:

`sudo yum -y install httpd`

Após confirmar a instalação, o yum instalará o Apache e todas as dependências necessárias. Quando a instalação estiver concluída, você estará pronto para iniciar o serviço.

# Passo 2 — Verificando seu Servidor Web

O Apache não inicia automaticamente no CentOS depois que a instalação é concluída. Você precisará iniciar o processo do Apache manualmente:

`sudo systemctl start httpd`

Verifique se o serviço está sendo executado com o seguinte comando:

`sudo systemctl status httpd`

Você verá um status active quando o serviço estiver em execução.

Como você pode ver nesta saída, o serviço parece ter sido iniciado com sucesso. No entanto, a melhor maneira de testar isso é solicitar uma página do Apache.

Você pode acessar a página inicial padrão do Apache para confirmar que o software está sendo executado corretamente através do seu endereço IP. Se você não souber o endereço IP do seu servidor, poderá obtê-lo de algumas maneiras diferentes a partir da linha de comando.

Digite isto no prompt de comando do seu servidor:

`hostname -I`

Esse comando exibirá todos os endereços de rede do host, assim você receberá um retorno com alguns endereços IP separados por espaços. Você pode experimentar cada um em seu navegador para ver se eles funcionam.

Alternativamente, você pode usar o curl para solicitar seu IP através do icanhazip.com, que lhe dará seu endereço IPv4 público como visto de outro local na internet:

`curl -4 icanhazip.com`

Quando você tiver o endereço IP do seu servidor, insira-o na barra de endereços do seu navegador:

**http://ip_do_seu_servidor**

Você verá a página padrão do Apache do CentOS 7:
Default Apache page for CentOS 7

Esta página indica que o Apache está funcionando corretamente. Ela também inclui algumas informações básicas sobre arquivos importantes do Apache e sobre localizações de diretórios. Agora que o serviço está instalado e em execução, você pode usar diferentes comandos `systemctl` para gerenciar o serviço.

# Passo 3 — Gerenciando o Processo do Apache

Agora que você tem seu servidor web funcionando, vamos passar por alguns comandos básicos de gerenciamento.

Para parar seu servidor web, digite:

`sudo systemctl stop httpd`

Para iniciar o servidor web quando ele estiver parado, digite:

`sudo systemctl start httpd`

Para parar e iniciar o serviço novamente, digite:

`sudo systemctl restart httpd`

Se você estiver simplesmente fazendo alterações de configuração, o Apache pode muita vezes recarregar sem perder conexões. Para fazer isso, use este comando:

`sudo systemctl reload httpd`

Por padrão, o Apache é configurado para iniciar automaticamente quando o servidor é inicializado. Se isso não é o que você deseja, desabilite esse comportamento digitando:

`sudo systemctl disable httpd`

Para reativar o serviço para iniciar na inicialização, digite:

`sudo systemctl enable httpd`

O Apache agora será iniciado automaticamente quando o servidor inicializar novamente.

A configuração padrão do Apache permitirá que seu servidor hospede um único site. Se você planeja hospedar vários domínios em seu servidor, precisará configurar virtual hosts em seu servidor Apache.
