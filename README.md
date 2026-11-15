# Aula 7 – Computação em Nuvem
## Secrets e Controle de Acesso no Kubernetes

### Introdução

Nesta aula, aprendemos um pouco mais sobre segurança dentro do Kubernetes, principalmente sobre como armazenar informações confidenciais e controlar o acesso aos recursos do ambiente.

Dando continuidade ao conteúdo da aula anterior, em que trabalhamos com configurações e armazenamento, estudamos como utilizar o Secret para guardar informações sensíveis e como definir quais usuários ou aplicações podem acessar determinados recursos.

Durante a explicação da professora, também conhecemos o ServiceAccount, as Roles e os RoleBindings, que ajudam a organizar e controlar as permissões dentro do Kubernetes.

### O que vimos na aula?

Durante o conteúdo teórico, estudamos os seguintes assuntos:

- **ConfigMap e Secret:** aprendemos a diferença entre os dois. O ConfigMap é utilizado para guardar informações de configuração que não são confidenciais, enquanto o Secret é utilizado para armazenar informações sensíveis, como senhas e credenciais.
- **Secret:** vimos como uma aplicação pode receber uma informação confidencial por meio de um arquivo disponibilizado dentro de um Pod.
- **ServiceAccount:** entendemos que funciona como uma identidade utilizada por aplicações e processos que precisam acessar a API do Kubernetes.
- **Role:** aprendemos que serve para definir quais ações podem ser realizadas em determinados recursos dentro de um namespace.
- **RoleBinding:** vimos que faz a ligação entre uma Role e uma identidade, permitindo que ela utilize as permissões configuradas.
- **RBAC:** conhecemos esse mecanismo de controle de acesso, que permite definir o que cada identidade pode ou não fazer dentro do Kubernetes.
- **Princípio do menor privilégio:** aprendemos a importância de conceder somente as permissões necessárias, evitando liberar acessos que não precisam ser utilizados.

### O que fizemos nas aulas práticas?

Durante a prática, utilizamos o Kubernetes Playground pelo Killercoda para realizar algumas configurações e testar os recursos estudados.

**1. Criando um Namespace e um Secret**

Começamos verificando os Nodes do ambiente para conferir se estavam funcionando corretamente.

Depois, criamos um namespace chamado `aula7`, para organizar os recursos utilizados durante a atividade.

Em seguida, trabalhamos com a criação de um Secret chamado `credencial-demo`, que seria utilizado para armazenar uma senha fictícia.

Nessa etapa, tivemos um pequeno erro ao executar o comando, pois o parâmetro responsável por armazenar a senha acabou sendo separado do comando principal. Com isso, o Secret foi criado, mas ficou sem nenhuma informação.

**2. Criando um Pod para utilizar o Secret**

Depois, criamos um arquivo chamado `pod-secret.yaml`, configurando um Pod com o nome `leitor-secret`.

Nesse arquivo, utilizamos a imagem BusyBox e configuramos um volume para disponibilizar as informações do Secret dentro da pasta `/segredos`.

Em seguida, aplicamos o arquivo e aguardamos o Pod ficar pronto.

Ao tentar visualizar o arquivo da senha, recebemos uma mensagem informando que ele não existia. Isso aconteceu porque o Secret criado anteriormente estava vazio.

Mesmo assim, conseguimos entender como funciona a utilização de um Secret dentro de um Pod.

**3. Criando uma ServiceAccount**

Na próxima etapa, criamos uma ServiceAccount chamada `leitor`.

Com isso, começamos a trabalhar com a parte de identificação e controle de acesso do Kubernetes.

Entendemos que essa identidade pode ser utilizada por aplicações e processos que precisam acessar os recursos do ambiente.

**4. Criando uma Role e um RoleBinding**

Depois, criamos uma Role chamada `consulta-pods`, permitindo que a ServiceAccount pudesse consultar e listar os Pods dentro do namespace `aula7`.

As permissões utilizadas foram `get` e `list`.

Em seguida, criamos um RoleBinding chamado `vinculo-leitor`, fazendo a ligação entre a Role `consulta-pods` e a ServiceAccount `leitor`.

Assim, conseguimos definir quais ações essa identidade poderia realizar.

**5. Testando as permissões**

Depois de configurar as permissões, utilizamos o comando `kubectl auth can-i` para verificar o que a ServiceAccount poderia fazer.

Realizamos dois testes:

- Consultar os Pods utilizando `get`: o resultado foi `yes`.
- Excluir os Pods utilizando `delete`: o resultado foi `no`.

Com esses testes, conseguimos confirmar que a identidade tinha permissão para consultar os Pods, mas não poderia excluí-los.

**6. Realizando o desafio prático**

No desafio, atualizamos a Role `consulta-pods`, adicionando uma nova permissão chamada `watch`.

Essa permissão permite acompanhar alterações nos Pods.

Depois de atualizar a Role, executamos novamente o comando de verificação para conferir se a ServiceAccount tinha recebido essa permissão.

O resultado foi `yes`, confirmando que a atualização havia funcionado corretamente.

**7. Finalizando a atividade**

Depois de concluir os testes, realizamos a limpeza do ambiente, excluindo o namespace `aula7`.

Com isso, os recursos criados durante a atividade, como o Pod, o Secret, a ServiceAccount e os objetos de controle de acesso, foram removidos.

Por último, verificamos se o namespace ainda existia e recebemos uma mensagem informando que ele não foi encontrado, confirmando que a exclusão havia sido realizada.

### O que aprendi com essa aula?

Com essa aula, consegui entender melhor como funciona a segurança e o controle de acesso dentro do Kubernetes.

Aprendi que o Secret é utilizado para disponibilizar informações sensíveis às aplicações e que o ServiceAccount funciona como uma identidade para acessar os recursos do ambiente.

Também consegui compreender melhor a diferença entre Role e RoleBinding. A Role define as permissões, enquanto o RoleBinding faz a ligação dessas permissões com uma identidade.

O que mais me chamou a atenção foi a parte dos testes de permissões, principalmente quando conseguimos consultar os Pods, mas não tínhamos autorização para excluí-los.

Mesmo com o erro durante a criação do Secret, consegui acompanhar as outras etapas e entender a importância de configurar corretamente cada recurso.

Foi uma aula importante para compreender melhor como podemos proteger informações e controlar os acessos dentro de um ambiente Kubernetes.

---

**Aula 07 – Computação em Nuvem**
