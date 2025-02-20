# Beqa (BEQA) - ERC-20 Token

## Descrição
**Beqa (BEQA)** é um token ERC-20 desinflacionário desenvolvido na rede **Polygon Mainnet**, seguindo padrões da OpenZeppelin. O contrato implementa funcionalidades essenciais para um token moderno, incluindo permissões de queima, assinatura off-chain (permit) e governança via propriedade (Ownable).

## Características Principais
- **Nome do Token:** Beqa
- **Símbolo:** BEQA
- **Fornecimento Inicial:** 50.000.000 BEQA
- **Decimais:** 18
- **Compatível com OpenZeppelin Contracts ^5.0.0**
- **Extensões Implementadas:**
  - `ERC20` - Padrão básico ERC-20.
  - `ERC20Burnable` - Permite que tokens sejam queimados.
  - `ERC20Permit` - Suporte para assinaturas off-chain.
  - `Ownable` - Controle de propriedade e governança.

## Implementação do Contrato
O contrato **Beqa** foi projetado para ser gerenciado por um proprietário inicial definido na implantação. Esse proprietário pode cunhar novos tokens conforme necessário.

```solidity
contract Beqa is ERC20, ERC20Burnable, Ownable, ERC20Permit {
    constructor(address initialOwner)
        ERC20("Beqa", "BEQA")
        Ownable(initialOwner)
        ERC20Permit("Beqa")
    {
        _mint(msg.sender, 50000000 * 10 ** decimals());
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
}
```

## Funções
### 1. **Minting (Cunhagem)**
A função `mint` permite que o proprietário gere novos tokens e os envie para um endereço específico.
```solidity
function mint(address to, uint256 amount) public onlyOwner {
    _mint(to, amount);
}
```
**Parâmetros:**
- `to` - Endereço que receberá os tokens.
- `amount` - Quantidade de tokens a serem criados.

**Restrições:**
- Apenas o proprietário (`onlyOwner`) pode executar essa função.

### 2. **Burning (Queima)**
Os tokens podem ser permanentemente removidos da circulação pelo próprio titular, reduzindo a oferta total.
```solidity
function burn(uint256 amount) public {
    _burn(msg.sender, amount);
}
```
**Parâmetros:**
- `amount` - Quantidade de tokens a serem queimados.

### 3. **Permit (Assinaturas Off-Chain)**
A função `ERC20Permit` permite aprovação de transações sem que o usuário precise enviar uma transação on-chain, reduzindo custos com gas.

## Implantação na Polygon
O contrato foi projetado para ser implantado na **Polygon Mainnet** usando **Remix - Ethereum IDE**.

### **Passos para Implantar**
1. Acesse o [Remix Ethereum IDE](https://remix.ethereum.org/)
2. Carregue o arquivo do contrato `Beqa.sol`
3. Compilar com `Solidity ^0.8.22`
4. Selecionar **Injected Provider - MetaMask** e conectar à rede **Polygon Mainnet**
5. Implantar o contrato passando o endereço do proprietário inicial

## Licença
Este projeto está licenciado sob a [MIT License](https://opensource.org/licenses/MIT).