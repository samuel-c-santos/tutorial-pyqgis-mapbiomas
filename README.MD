# Automatização de Simbologia MapBiomas com PyQGIS

[![Tutorial Completo](https://img.shields.io/badge/Tutorial-Acesse%20Aqui-2563eb?style=for-the-badge)](https://samuel-c-santos.github.io/tutorial-pyqgis-mapbiomas/)

> Script Python para aplicação automatizada de simbologia oficial do MapBiomas (Coleção 10) em múltiplas camadas vetoriais usando PyQGIS.

[![Tutorial Preview](img/mockup.png)](https://samuel-c-santos.github.io/tutorial-pyqgis-mapbiomas/)

**[Acesse o tutorial completo e interativo](https://samuel-c-santos.github.io/tutorial-pyqgis-mapbiomas/)**

## Sobre o Projeto

Este repositório contém uma solução completa para automatizar a aplicação de simbologia padronizada em camadas MapBiomas. O processo manual de configurar cores e legendas para múltiplas camadas de análise temporal é tedioso e propenso a erros. Com este script PyQGIS, é possível aplicar a legenda oficial do MapBiomas em dezenas de camadas em questão de segundos.

### Funcionalidades

- Aplicação batch de simbologia em múltiplas camadas vetoriais
- Cores padronizadas conforme legenda oficial MapBiomas Coleção 10
- Suporte a camadas poligonizadas de uso e cobertura do solo
- Código documentado e reutilizável
- Dados de exemplo incluídos (Bragança-PA)

## Pré-requisitos

- **QGIS 3.x** instalado
- Conhecimento básico de geoprocessamento
- Dados raster do MapBiomas (Coleção 10 ou superior)
- Python habilitado no QGIS

## Estrutura do Repositório

```
.
├── img/                          # Imagens do tutorial
├── script_simbologia_pyqgis.py  # Script principal PyQGIS
├── Legenda-Colecao-10-Legend-Code.csv  # Legenda oficial (CSV)
├── Legenda-Colecao-10-Legend-Code.pdf  # Legenda oficial (PDF)
├── tif/                          # Dados raster de exemplo
│   └── mapbiomas-brazil-collection-100-braganca-2024.tif
├── shape/                        # Dados vetoriais processados
│   └── mapbiomas-brazil-collection-100-braganca-2024.*
└── index.html                    # Tutorial interativo
```

## Instalação e Uso

### 1. Download dos Arquivos

Clone este repositório ou baixe os arquivos necessários:

```bash
git clone https://github.com/samuel-c-santos/tutorial-pyqgis-mapbiomas.git
```

### 2. Preparação dos Dados

**Poligonizar o Raster:**
- Carregue o raster MapBiomas no QGIS
- Acesse: `Raster → Conversão → Poligonizar (Raster para Vetor)`
- Configure o campo `DN` para armazenar os Code IDs

**Limpar Bordas:**
- Aplique filtro: `"DN" != 0`
- Exporte apenas as feições válidas

**Fazer Join com a Legenda:**
- Adicione o CSV `Legenda-Colecao-10-Legend-Code.csv` ao projeto
- Configure join entre campo `DN` e `Code ID`
- Marque "Campo personalizado e prefixo do nome" e remova o prefixo
- Salve permanentemente o shapefile com os dados unidos

### 3. Executar o Script

**No Console Python do QGIS:**

1. Abra o Console Python (`Ctrl+Alt+P`)
2. Clique em "Mostrar Editor"
3. Abra o arquivo `script_simbologia_pyqgis.py`
4. Edite a lista `LAYER_NAMES` com os nomes das suas camadas
5. Execute o script

**Exemplo de configuração:**

```python
LAYER_NAMES = [
    "mapbiomas-brazil-collection-100-braganca-2024",
    "mapbiomas-brazil-collection-100-braganca-2023",
    "mapbiomas-brazil-collection-100-braganca-2022"
]
```

### 4. Resultado

Todas as camadas listadas terão a simbologia oficial do MapBiomas aplicada automaticamente, com cores padronizadas e categorias corretamente classificadas.

## Script Principal

O script `script_simbologia_pyqgis.py` realiza as seguintes operações:

1. Lê valores únicos dos campos `COLEÇÃO 10 - CLASSES` e `Hexacode Number`
2. Cria categorias de simbologia baseadas nas informações da legenda
3. Aplica o renderer categorizado em todas as camadas especificadas
4. Atualiza a visualização do mapa automaticamente

## Legenda Oficial

O arquivo CSV incluído é uma extração do PDF oficial da legenda da **Coleção 10 do MapBiomas**, contendo:

- **Code ID**: Identificador numérico da classe
- **COLEÇÃO 10 - CLASSES**: Nome da classe em português
- **Hexacode Number**: Código hexadecimal da cor oficial

## Dados de Exemplo

O repositório inclui dados de exemplo para a região de **Bragança-PA**:

- Raster: `mapbiomas-brazil-collection-100-braganca-2024.tif`
- Shapefile processado: `mapbiomas-brazil-collection-100-braganca-2024.shp`

Estes dados podem ser utilizados para testar o workflow completo descrito no tutorial.

## Vantagens da Automação

- **Velocidade**: Aplica simbologia em dezenas de camadas em segundos
- **Padronização**: Garante cores consistentes com a legenda oficial
- **Reprodutibilidade**: Mesmos parâmetros geram mesmos resultados
- **Escalabilidade**: Funciona para qualquer quantidade de camadas
- **Redução de Erros**: Elimina configuração manual repetitiva

## Solução de Problemas

### Erro: Campos não encontrados

**Causa**: Nomes dos campos no script não correspondem aos nomes reais.

**Solução**: Verifique os nomes na tabela de atributos e ajuste as variáveis `CLASSIFICATION_FIELD` e `HEXACODE_FIELD`.

### Cores não aparecem

**Causa**: Códigos hexadecimais sem o símbolo `#`.

**Solução**: O script já trata isso automaticamente, mas verifique a integridade do CSV.

### Script não encontra camadas

**Causa**: Nomes das camadas no script diferem dos nomes no projeto.

**Solução**: Use os nomes exatos do painel de camadas (sem extensão .shp).

## Aplicações Adicionais

Este workflow pode ser expandido para:

- Criação de layouts de mapa automatizados com QGIS Atlas
- Exportação de estatísticas de área por classe de uso
- Geração de mapas de mudança de uso do solo temporal
- Integração com pipelines de processamento geoespacial

## Referências

- [MapBiomas Brasil](https://mapbiomas.org/)
- [Documentação PyQGIS](https://qgis.org/pyqgis/)
- [QGIS Official Site](https://qgis.org/)

## Licença

Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.

## Autor

**Samuel Santos**

- Portfolio: [samuel-c-santos.github.io](https://samuel-c-santos.github.io/)
- LinkedIn: [samuel-c-santos](https://linkedin.com/in/samuel-c-santos)
- GitHub: [@samuel-c-santos](https://github.com/samuel-c-santos)
- Email: samuelsantosambiental@gmail.com

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para:

1. Fazer fork do projeto
2. Criar uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abrir um Pull Request

---

**[Acesse o tutorial completo e interativo](https://samuel-c-santos.github.io/tutorial-pyqgis-mapbiomas/)**
