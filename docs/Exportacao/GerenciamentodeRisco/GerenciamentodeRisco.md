## Gerenciamento de Risco

### 🧾 Visão Geral
 
O menu **Gerenciamento de Risco** tem como objetivo identificar, registrar e acompanhar os riscos relacionados as análises da exportação, garantindo rastreabilidade e mitigação de impactos.

---

## Sumário

- [Principais Funcionalidades](GerenciamentodeRisco.md#%EF%B8%8F-principais-funcionalidades)
- [Interface do Sistema](GerenciamentodeRisco.md#%EF%B8%8F-interface-do-sistema)
    - [Tela de Busca de Risco](GerenciamentodeRisco.md#tela-de-busca-de-risco)
    - [Tela de Riscos da Analise](GerenciamentodeRisco.md#tela-de-riscos-da-analise)
    - [Tela de Pesquisa dos Riscos](GerenciamentodeRisco.md#tela-de-pesquisa-dos-riscos)
---

### ⚙️ Principais Funcionalidades

1. **Gerenciar de Riscos**
   - Permite gerar e salvar os riscos associados a uma análise.
   - Campos principais:
     - `Cliente`: Nome do cliente.
     - `Item Acabado`: Código do item da mangotex.
     - `Part Number`: Código do cliente.
     - `Data do Recebimento`: Data do envio mais o leadtime.
     - `Data EUA`: Data do pedido do cliente.
     - `Programa`: Quantidade solicitada pelo cliente.
     - `Estoque`: Valor do estoque.
     - `Ação`: Campo aberto para o usuário descrever a ação à ser tomada.

---

### 🖼️ Interface do Sistema

#### Tela de Busca de Risco
    O usuário deve selecionar a análise para gerar os risco.
![Tela de Busca de Risco](/images/Exportacao/GerenciamentodeRisco/GR_pesquisarAnalise.png)

#### Tela de Riscos da Analise
    Será realizada uma análise, e os riscos associados à análise selecionada serão exibidos na tela.
    Os potenciais riscos serão destacados em vermelho.
    O sistema permitirá ao usuário digitar e salvar a ação a ser tomada em relação a cada risco identificado.
![Tela de Riscos da Analise](/images/Exportacao/GerenciamentodeRisco/GR_tabela_risco.png)

#### Tela de Pesquisa dos Riscos
    O sistema permitirá realizar a pesquisa de riscos utilizando filtros específicos, possibilitando a busca por análise, item acabado, part number ou cliente.
    Também será possível aplicar filtros compostos para refinar os resultados.
![Tela de Pesquisa dos Riscos](/images/Exportacao/GerenciamentodeRisco/GR_pesquisaFiltros.png)


## Histórico de Versões
| Data        | Versão  |                        Alteração                           | Autor          |
|-------------|---------|------------------------------------------------------------|----------------|
| 13/11/2025  | v1.0    | Criação inicial da documentação do gerenciamento de risco  | Vitor Medeiros |

