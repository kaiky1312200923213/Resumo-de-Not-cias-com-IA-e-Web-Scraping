# Resumo-de-Not-cias-com-IA-e-Web-Scraping
import requests
from bs4 import BeautifulSoup
from agno.agent import Agent
from agno.models.openai import OpenAIChat

API_KEY = "SEU_API"

def extrair_artigo(url: str) -> str:
    """Extrai o texto principal de um artigo web."""
    headers = {"User-Agent": "Mozilla/5.0"}
    try:
        response = requests.get(url, headers=headers, timeout=10)
        response.raise_for_status()
        soup = BeautifulSoup(response.text, "html.parser")

        # Remove scripts e estilos
        for tag in soup(["script", "style", "nav", "footer", "header"]):
            tag.decompose()

        # Tenta pegar parágrafos do artigo
        paragrafos = soup.find_all("p")
        texto = " ".join(p.get_text(strip=True) for p in paragrafos if len(p.get_text(strip=True)) > 50)

        return texto[:3000] if texto else "Não foi possível extrair o conteúdo."
    except Exception as e:
        return f"Erro ao acessar a página: {e}"

agente = Agent(
    model=OpenAIChat(
        id="meta/llama-3.1-8b-instruct",
        api_key=API_KEY,
        base_url="https://integrate.api.nvidia.com/v1"
    ),
    instructions="""
    Você é um assistente especialista em resumir artigos de tecnologia.
    Quando receber um texto, resuma-o em exatamente 3 frases claras e objetivas em português.
    Foque nos pontos mais importantes do artigo.
    """
)

def main():
    print("=" * 55)
    print("   📰 Resumidor de Notícias com IA")
    print("=" * 55)

    # URL de um artigo público de tecnologia
    url = "https://www.tecmundo.com.br/inteligencia-artificial/o-que-e-inteligencia-artificial"

    print(f"\n🔗 Acessando: {url}\n")
    conteudo = extrair_artigo(url)

    if "Erro" in conteudo:
        print(conteudo)
        return

    print(f"✅ Conteúdo extraído ({len(conteudo)} caracteres)\n")
    print("-" * 55)
    print("🤖 Resumo gerado pela IA:\n")

    agente.print_response(f"Resuma este artigo em 3 frases:\n\n{conteudo}")

if _name_ == "_main_":
    main()
