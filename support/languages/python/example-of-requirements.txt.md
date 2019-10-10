# Creating your requirements.txt

## Como Funciona:

Segundo a [documentação do pip sobre arquivos requirements](https://pip.pypa.io/en/stable/user_guide/#requirements-files):

> “Requirements files” are files containing a list of items to be installed using pip install

 Ou seja, esse arquivo nada mais é do que um arquivo de texto, contendo uma lista de **itens/pacotes** para serem instalados durante o **`pip install`** durante o processo de deploy na Discloud.

### Vamos a um exemplo:

 Considerando esse `requirements.txt` aqui:

```text
-e git+https://github.com/jtemporal/caipyra.git@master#egg=caipyra
discord.py
seaborn==0.8.1
pandas>=0.18.1
```

1.  **-e git+https://github.com/jtemporal/caipyra.git@master\#egg=caipyra**: Dessa forma conseguimos instalar pacotes Python que estejam disponíveis no GitHub mas não no PyPI. Essa é uma dica muito legal quando por exemplo, você precisa da versão em desenvolvimento de um biblioteca ou quando você prefere usar um fork no lugar da versão tradicional do pacote. 
2. **discord.py**: Quando não especificamos uma versão, o **pip** sempre tentará instalar a versão mais recente do pacote especificado. 
3. **seaborn==0.8.1**: No caso do seaborn, estamos instalando a versão **`0.8.1`**. Fixar a versão dessa forma é interessante pois garante que o seu projeto vai sempre estar funcionando já que mudanças nos pacotes são indicadas pela alteração no número da versão. 
4.  **pandas&gt;=0.18.1**: Da mesma forma que o sinal de **`==`** define uma versão específica a ser instalada, quando usamos o sinal de **`>=`** nessa lista estamos dizendo que queremos instalar qualquer versão da biblioteca, nesse caso o pandas, seja ela a versão **`0.18.1`** ou uma mais recente. Interessante nesse caso é notar que você pode definir um intervalo de versões, por exemplo, **`pandas>=0.15.0,<=0.18.1`**.

## ✍ Como crio meu requirements.txt ?

Você pode usar o próprio **bloco de notas** para criar seu arquivo **`requirements.txt`**

![Criando um novo documento de texto e renomeando para &quot;requirements&quot;](../../../.gitbook/assets/image%20%285%29.png)

![Exemplo de do arquivo criado com algumas depend&#xEA;ncias j&#xE1; definidas  ](../../../.gitbook/assets/image%20%282%29.png)

## ✍ Gerando automaticamente o arquivo requirements.txt

 Um jeito simples de criar o seu próprio arquivo de dependências é usando o comando **`pip freeze`** da seguinte forma:

```text
pip freeze > requirements.txt
```

O comando **`pip freeze`** lista no terminal os pacotes **Python** instalados no seu ambiente já no formato que o **pip install** consegue entender, ao associá-lo com o operador de redireção `>` você consegue escrever a mesma lista que aparece no terminal dentro do arquivo de texto.

![](../../../.gitbook/assets/capturar%20%284%29.PNG)

{% hint style="success" %}
#### Massa né? Agora é só criar arquivos de dependências para todos projetos 😜
{% endhint %}

