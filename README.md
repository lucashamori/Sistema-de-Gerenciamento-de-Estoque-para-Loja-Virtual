# Sistema-de-Gerenciamento-de-Estoque-para-Loja-Virtual
Este sistema em Python permite gerenciar o estoque de produtos de uma loja virtual. Ele inclui funcionalidades para adicionar, buscar, listar, atualizar e remover produtos do estoque, além de registrar vendas e gerar relatórios. Esse código foi criado a partir de um estudo de métodos e POO.
## Estrutura do Projeto

O projeto contém duas classes principais: `Produto` e `Loja`.

### Classe Produto

Representa um produto na loja.

### Atributos

- `codigo (int)`: Código do produto.
- `nome (str)`: Nome do produto.
- `preco (float)`: Preço do produto.
- `quantidade (int)`: Quantidade disponível do produto.

### Métodos

- `__init__(self, codigo, nome, preco, quantidade)`: Inicializa um novo produto.
- `atualizar_preco(self, novo_preco)`: Atualiza o preço do produto.
- `adicionar_estoque(self, quantidade)`: Adiciona uma quantidade ao estoque do produto.
- `remover_estoque(self, quantidade)`: Remove uma quantidade do estoque do produto.
- `create_auth(cls, codigo, nome, preco, quantidade)`: Classe de fábrica para criar um novo produto.
- `calcular_valor_total(produtos)`: Calcula o valor total de uma lista de produtos.

### Classe Loja

Representa uma loja virtual.

### Atributos

- `nome_loja (str)`: Nome da loja.
- `produtos (dict)`: Dicionário de produtos cadastrados na loja.
- `vendas (list)`: Lista de vendas realizadas.

### Métodos

- `__init__(self, nome_loja)`: Inicializa uma nova loja.
- `adicionar_produto(self, produto)`: Adiciona um produto ao estoque da loja.
- `buscar_produto_por_codigo(self, codigo)`: Busca um produto pelo código.
- `listar_produtos(self)`: Lista todos os produtos cadastrados na loja.
- `verificar_disponibilidade(self, codigo)`: Verifica se um produto está disponível em estoque.
- `registrar_venda(self, codigo, quantidade)`: Registra uma venda de um produto.
- `gerar_relatorio_vendas(self)`: Gera um relatório das vendas realizadas.

## Exemplo de Uso

```python
pythonCopiar código
# Desenvolver um sistema em Python para gerenciar produtos em um estoque de uma loja virtual.

class Produto:
    """
    Classe que representa um produto na loja.

    Atributos:
    codigo (int): Código do produto.
    nome (str): Nome do produto.
    preco (float): Preço do produto.
    quantidade (int): Quantidade disponível do produto.
    """

    def __init__(self, codigo, nome, preco, quantidade):
        """
        Inicializa um novo produto com os dados fornecidos.

        Args:
        codigo (int): Código do produto.
        nome (str): Nome do produto.
        preco (float): Preço do produto.
        quantidade (int): Quantidade disponível do produto.
        """
        self.codigo = codigo
        self.nome = nome
        self.preco = preco
        self.quantidade = quantidade

    def atualizar_preco(self, novo_preco):
        """
        Atualiza o preço do produto.

        Args:
        novo_preco (float): Novo preço do produto.
        """
        self.preco = novo_preco

    def adicionar_estoque(self, quantidade):
        """
        Adiciona uma quantidade ao estoque do produto.

        Args:
        quantidade (int): Quantidade a ser adicionada.
        """
        self.quantidade += quantidade

    def remover_estoque(self, quantidade):
        """
        Remove uma quantidade do estoque do produto.

        Args:
        quantidade (int): Quantidade a ser removida.

        Raises:
        ValueError: Se a quantidade a ser removida é maior que a disponível no estoque.
        """
        if self.quantidade >= quantidade:
            self.quantidade -= quantidade
        else:
            print("Quantidade insuficiente em estoque.")

    @classmethod
    def create_auth(cls, codigo, nome, preco, quantidade):
        """
        Cria um novo produto com os dados fornecidos.

        Args:
        codigo (int): Código do produto.
        nome (str): Nome do produto.
        preco (float): Preço do produto.
        quantidade (int): Quantidade disponível do produto.

        Returns:
        Produto: Uma nova instância da classe Produto.
        """
        return cls(codigo, nome, preco, quantidade)

    @staticmethod
    def calcular_valor_total(produtos):
        """
        Calcula o valor total de uma lista de produtos.

        Args:
        produtos (list): Lista de instâncias da classe Produto.

        Returns:
        float: Valor total dos produtos.
        """
        total = 0
        for produto in produtos:
            total += produto.preco * produto.quantidade
        return total

class Loja:
    """
    Classe que representa uma loja virtual.

    Atributos:
    nome_loja (str): Nome da loja.
    produtos (dict): Dicionário de produtos cadastrados na loja.
    vendas (list): Lista de vendas realizadas.
    """

    def __init__(self, nome_loja):
        """
        Inicializa uma nova loja com o nome fornecido.

        Args:
        nome_loja (str): Nome da loja.
        """
        self.nome_loja = nome_loja
        self.produtos = {}
        self.vendas = []

    def adicionar_produto(self, produto):
        """
        Adiciona um produto ao estoque da loja.

        Args:
        produto (Produto): Instância da classe Produto a ser adicionada.

        Raises:
        ValueError: Se já existir um produto com o mesmo código.
        """
        if produto.codigo in self.produtos:
            print("Já existe um produto com esse código.")
        else:
            self.produtos[produto.codigo] = produto
            print("Produto adicionado com sucesso.")

    def buscar_produto_por_codigo(self, codigo):
        """
        Busca um produto pelo código.

        Args:
        codigo (int): Código do produto.

        Returns:
        Produto: Instância da classe Produto, se encontrada. Caso contrário, retorna None.
        """
        if codigo in self.produtos:
            return self.produtos[codigo]
        else:
            print("Produto não encontrado.")
            return None

    def listar_produtos(self):
        """
        Lista todos os produtos cadastrados na loja.
        """
        if not self.produtos:
            print("Nenhum produto cadastrado.")
        else:
            for produto in self.produtos.values():
                print(f"Código: {produto.codigo}, Nome: {produto.nome}, Preço: {produto.preco}, Quantidade: {produto.quantidade}")

    def verificar_disponibilidade(self, codigo):
        """
        Verifica se um produto está disponível em estoque.

        Args:
        codigo (int): Código do produto.

        Returns:
        str: "Estoque disponível." se o produto está disponível, caso contrário "Produto não disponível ou fora de estoque."
        """
        produto = self.buscar_produto_por_codigo(codigo)
        if produto and produto.quantidade > 0:
            return "Estoque disponível."
        return "Produto não disponível ou fora de estoque."

    def registrar_venda(self, codigo, quantidade):
        """
        Registra uma venda de um produto.

        Args:
        codigo (int): Código do produto.
        quantidade (int): Quantidade a ser vendida.

        Raises:
        ValueError: Se a quantidade a ser vendida é maior que a disponível no estoque.
        """
        produto = self.buscar_produto_por_codigo(codigo)
        if produto and produto.quantidade >= quantidade:
            produto.remover_estoque(quantidade)
            self.vendas.append((produto.codigo, quantidade, produto.preco * quantidade))
            print(f"Venda realizada com sucesso. Quantidade de {produto.nome} vendida: {quantidade}")
        else:
            print("Quantidade insuficiente em estoque.")

    def gerar_relatorio_vendas(self):
        """
        Gera um relatório das vendas realizadas.
        """
        if self.vendas:
            total_vendas = sum(venda[2] for venda in self.vendas)
            print(f"Total de vendas: R$ {total_vendas}")
            for venda in self.vendas:
                produto = self.buscar_produto_por_codigo(venda[0])
                if produto:
                    print(f"Código: {venda[0]}, Nome: {produto.nome}, Quantidade: {venda[1]}, Valor Total: R$ {venda[2]}")
        else:
            print("Nenhuma venda registrada.")

# Exemplo de uso
if __name__ == "__main__":
    # Criação de loja
    loja = Loja("Loja Virtual do Senac")  # Corrigido para instanciar a classe Loja

    # Criação de produtos
    produto1 = Produto.create_auth(1, "Notebook", 1500, 5)
    produto2 = Produto.create_auth(2, "Mouse", 50, 10)
    produto3 = Produto.create_auth(3, "Teclado", 100, 8)

    # Adicionando produtos à loja
    loja.adicionar_produto(produto1)
    loja.adicionar_produto(produto2)
    loja.adicionar_produto(produto3)

    # Listando produtos
    loja.listar_produtos()

    # Atualizando preço de um produto
    produto2.atualizar_preco(70)

    # Buscar produto por código
    produto_buscado = loja.buscar_produto_por_codigo(2)
    if produto_buscado:
        print(f"Nome: {produto_buscado.nome}, Preço: {produto_buscado.preco}")
    else:
        print("Produto não encontrado.")

    # Remover produtos
    loja.produtos[2].remover_estoque(3)
    loja.produtos[3].remover_estoque(5)

    # Listando produtos após remoção
    loja.listar_produtos()

    # Calculando valor total dos produtos
    total_produtos = Produto.calcular_valor_total(loja.produtos.values())
    print(f"Valor total dos produtos: {total_produtos}")

    # Verificando disponibilidade de produto
    disponibilidade = loja.verificar_disponibilidade(1)
    print(disponibilidade)

    # Registrando venda
    loja.registrar_venda(1, 2)
    loja.registrar_venda(2, 3)

    # Gerando relatório de vendas
    print("\nRelatório de Vendas:")
    loja.gerar_relatorio_vendas()

```

## Executando o Código
