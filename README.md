# Resumidor de Notícias com IA e Web Scraping

**Autor:** Kaiky Yoshio Ono Marins  
**Categoria:** Python · Web scraping · IA generativa  
**Status:** Protótipo de estudo

## Visão geral

Experimento em Python que acessa uma página pública, extrai texto de artigos e envia o conteúdo para um agente de IA gerar um resumo em português. O exemplo usa Requests e BeautifulSoup para obter o texto e Agno para organizar a chamada ao modelo.

## Fluxo do exemplo

1. Acessa uma URL pública com uma requisição HTTP.
2. Analisa o HTML e remove elementos de navegação e scripts.
3. Extrai os parágrafos relevantes.
4. Envia o texto extraído ao agente para resumir em três frases.

## Tecnologias

- Python
- Requests
- BeautifulSoup
- Agno
- Endpoint compatível com OpenAI / NVIDIA NIM

## Material e execução

O código original está em [MATERIAL-ORIGINAL.txt](./MATERIAL-ORIGINAL.txt). Instale as bibliotecas usadas no exemplo e configure a chave de API localmente antes de executar. Respeite os termos de uso, limites de acesso e políticas do site consultado; scraping não deve sobrecarregar serviços.

© 2026 Kaiky Yoshio Ono Marins.