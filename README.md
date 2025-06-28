# Gerenciamento de Máquinas Virtuais no Azure

Este repositório contém anotações, comandos e boas práticas para o gerenciamento de Máquinas Virtuais (VMs) na plataforma Microsoft Azure.

## 📘 Tópicos Abordados

- Criação de VMs
- Conexão e acesso remoto
- Gerenciamento de estados (start/stop/restart)
- Redimensionamento de VMs
- Gerenciamento de disco
- Monitoramento e diagnóstico
- Backup e recuperação
- Automação com Azure CLI e PowerShell

---

## 🚀 Criação de VMs

### Via Azure Portal
1. Acesse [portal.azure.com](https://portal.azure.com)
2. Navegue até "Máquinas Virtuais"
3. Clique em **Criar**
4. Selecione:
   - Imagem (ex: Ubuntu, Windows Server)
   - Tamanho (SKU)
   - Rede virtual e grupo de segurança
   - Chave SSH ou senha de acesso

### Via Azure CLI
```bash
az vm create \
  --resource-group MeuGrupoDeRecursos \
  --name MinhaVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

---

## 🔐 Conexão com a VM

### Linux (via SSH)
```bash
ssh azureuser@<ip_publico>
```

### Windows (via RDP)
- Use o Remote Desktop (mstsc)
- Conecte com o IP público e as credenciais definidas

---

## ⚙️ Gerenciamento de Estados

```bash
az vm start --name MinhaVM --resource-group MeuGrupoDeRecursos
az vm stop --name MinhaVM --resource-group MeuGrupoDeRecursos
az vm restart --name MinhaVM --resource-group MeuGrupoDeRecursos
az vm deallocate --name MinhaVM --resource-group MeuGrupoDeRecursos
```

---

## 📏 Redimensionamento de VMs

> Pare a VM antes de redimensionar.

```bash
az vm resize \
  --resource-group MeuGrupoDeRecursos \
  --name MinhaVM \
  --size Standard_DS2_v2
```

---

## 💾 Gerenciamento de Disco

- Adicionar disco:
```bash
az vm disk attach \
  --resource-group MeuGrupoDeRecursos \
  --vm-name MinhaVM \
  --name NovoDisco \
  --new \
  --size-gb 128
```

---

## 📊 Monitoramento

- Habilite o monitoramento padrão com Azure Monitor
- Logs e métricas estão disponíveis via Azure Portal

```bash
az monitor metrics list \
  --resource /subscriptions/<id>/resourceGroups/<grupo>/providers/Microsoft.Compute/virtualMachines/<vm>
```

---

## 🔄 Backup e Recuperação

- Configure o Azure Backup via portal ou CLI
- Crie políticas de backup automáticas

```bash
az backup protection enable-for-vm \
  --resource-group MeuGrupoDeRecursos \
  --vault-name MeuCofreBackup \
  --vm MinhaVM \
  --policy-name DefaultPolicy
```

---

## 🤖 Automação com Scripts

- **Azure CLI**: Ideal para scripts simples e integração com pipelines CI/CD
- **PowerShell**: Recomendado para ambientes Windows

Exemplo em PowerShell:
```powershell
Start-AzVM -ResourceGroupName "MeuGrupo" -Name "MinhaVM"
```

---

## 📚 Referências

- [Documentação oficial do Azure](https://learn.microsoft.com/azure/virtual-machines/)
- [Azure CLI - VMs](https://learn.microsoft.com/cli/azure/vm)
- [Azure PowerShell](https://learn.microsoft.com/powershell/azure/)

---

## 🧾 Notas Finais

- Mantenha suas credenciais e chaves privadas seguras
- Automatize tarefas recorrentes com scripts ou Azure Automation
- Use tags para organização e controle de custos
- Avalie o uso do Azure Advisor para recomendações de desempenho e segurança
