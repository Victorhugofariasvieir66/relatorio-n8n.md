# Relatório TryHackMe — n8n: CVE-2025-68613

**Vulnerabilidade:** CVE-2025-68613  
**Publicação:** 19/12/2025  
**CVSS:** 9.9 (Crítico)

## Resumo
Relatório da exploração e análise da vulnerabilidade de injeção de expressão no n8n que permite execução remota de código (RCE). Documenta ambiente, passos, payloads testados, evidências e recomendações.

## Objetivos
- Reproduzir a exploração na room TryHackMe.  
- Documentar comandos e evidências.  
- Propor mitigação e detecção.

## Ambiente de teste
- SO: Linux (preencher distro e versão)  
- Versão n8n testada: (preencher)  
- Rede: ambiente isolado / VM

## Ferramentas
- curl, nc, wget, jq  
- Burp Suite / proxy HTTP  
- VM local para testes

## Passos realizados
1. **Reconhecimento**  
   - Identificação de endpoints expostos e versão do n8n.  
2. **Enumeração**  
   - Mapeamento de rotas e endpoints de workflows.  
3. **Exploração**  
   - Envio de payloads de expressão que avaliam código JavaScript e invocam `child_process`.  
   - Exemplo de padrão malicioso: `this.process.mainModule.require('child_process').execSync(...)`  
4. **Pós-exploração**  
   - Monitoramento de criação de processos e evidências de execução.  
5. **Limpeza**  
   - Remoção de artefatos e restauração do ambiente.

## Exemplos de comandos
```bash
# checar saúde/versão (exemplo)
curl -s http://TARGET:5678/health

# exemplo genérico de POST para endpoint de workflows
curl -X POST http://TARGET:5678/rest/workflows -H "Content-Type: application/json" -d '{"some":"payload"}'
