# silver-barnacle
import os
from open_deep_search import OpenDeepSearchTool  # Verifique o nome correto do módulo!
from lite_llm import LiteLLMModel
from real_module import CodeAgent  # Substitua pelo módulo correto

# Definir variáveis de ambiente
os.environ["SERPER_API_KEY"] = "key"
os.environ["OPENROUTER_API_KEY"] = "key"
os.environ["JINA_API_KEY"] = "key"

# Criar agente de pesquisa
search_agent = OpenDeepSearchTool("openrouter/google/gemini-2.0-flash-001", reranker="jina")

# Verificar se precisa ser configurado
if hasattr(search_agent, "is_initialized") and not search_agent.is_initialized:
    search_agent.setup()

# Criar modelo
model = LiteLLMModel("openrouter/google/gemini-2.0-flash-001", temperature=0.2)

# Criar agente de código
code_agent = CodeAgent(tools=[search_agent], model=model)

# Definir consulta
query = "How long would a cheetah at full speed take to run the length of Pont Alexandre III?"
result = code_agent.run(query)

# Exibir resultado
print(result)
