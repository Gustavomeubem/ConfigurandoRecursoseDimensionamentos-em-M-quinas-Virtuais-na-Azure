# **Configurando Recursos e Dimensionamento de Máquinas Virtuais no Azure**  

Este guia explica como configurar, dimensionar e otimizar Máquinas Virtuais (VMs) no Microsoft Azure para diferentes cargas de trabalho.  

---

## **📌 Pré-requisitos**  
✔️ Conta ativa no Azure ([Crie uma gratuitamente](https://azure.microsoft.com/free/))  
✔️ Acesso ao [Portal Azure](https://portal.azure.com)  
✔️ Permissões para criar e gerenciar recursos  

---

## **🔧 Configuração Básica de uma VM**  

### **1. Seleção da Imagem e Tamanho**  
- **Imagens disponíveis**:  
  - Windows Server (2019, 2022)  
  - Linux (Ubuntu, CentOS, Red Hat, Debian)  
  - Imagens pré-configuradas (SQL Server, SAP, Machine Learning)  

- **Tamanhos recomendados**:  
  - **B1s (Burstable)**: Testes e desenvolvimento  
  - **D2s v3/D4s v3**: Cargas de trabalho gerais  
  - **Fsv2**: Computação de alto desempenho  
  - **NVv4/NCas_T4_v3**: GPU para IA e processamento gráfico  

📌 **Dica**: Use a [Calculadora de Preços do Azure](https://azure.microsoft.com/pricing/calculator/) para estimar custos.  

---

### **2. Configuração de Rede e Segurança**  
- **Rede Virtual (VNet)**:  
  - Crie ou selecione uma VNet existente.  
  - Defina sub-redes para isolamento lógico.  

- **Grupo de Segurança de Rede (NSG)**:  
  - Regras de entrada/saída (ex: RDP 3389, SSH 22).  
  - Restrinja acesso a IPs específicos.  

- **IP Público**:  
  - Atribua um IP público se a VM precisar de acesso externo.  

---

### **3. Armazenamento (Discos)**  
- **Tipos de disco**:  
  - **HDD Standard**: Custo baixo, desempenho moderado.  
  - **SSD Standard**: Balanceado entre custo e desempenho.  
  - **SSD Premium**: Alta IOPS e baixa latência (ideal para bancos de dados).  

- **Configurações recomendadas**:  
  - **Disco do SO**: SSD Premium (128 GB ou mais).  
  - **Discos de dados**: Adicione conforme necessidade (ex: 1 TB SSD para armazenamento).  

---

## **⚡ Dimensionamento Automático (Auto Scaling)**  

### **1. Escalando Verticalmente (Aumentando Recursos)**  
- **Mudança de tamanho da VM**:  
  - No Portal Azure, vá para a VM → **Tamanho**.  
  - Escolha um novo tamanho (ex: de **B2s** para **D4s v3**).  

⚠️ **Atenção**: A VM será reiniciada durante o redimensionamento.  

### **2. Escalando Horizontalmente (Conjuntos de Escala de VM)**  
- **Azure Virtual Machine Scale Sets (VMSS)**:  
  - Permite criar várias VMs idênticas com balanceamento de carga.  
  - Configuração automática baseada em métricas (CPU, memória).  

📌 **Exemplo de configuração**:  
```bash
az vmss create \
  --resource-group MyResourceGroup \
  --name MyScaleSet \
  --image UbuntuLTS \
  --vm-sku Standard_B1s \
  --instance-count 2 \
  --autoscale-rules "scale out when CPU > 70% for 5 mins"
```

---

## **🔍 Monitoramento e Otimização**  

### **1. Azure Monitor**  
- **Métricas-chave**:  
  - Uso de CPU (%)  
  - Consumo de memória  
  - Latência de disco  

- **Alertas**: Configure notificações para:  
  - CPU > 80% por 10 minutos  
  - Espaço em disco < 20%  

### **2. Azure Advisor**  
- Recomendações para:  
  - Redução de custos (desligar VMs ociosas).  
  - Melhorias de segurança (atualizações pendentes).  

---

## **💡 Melhores Práticas**  

✅ **Use Discos Gerenciados** para melhor confiabilidade.  
✅ **Habilite Backup** para recuperação de desastres.  
✅ **Aplique Tags** para organização (ex: `Ambiente: Produção`).  
✅ **Desligue VMs não utilizadas** para economizar custos.  

---

## **🗑️ Limpeza de Recursos**  
Para evitar cobranças indesejadas:  
1. Vá para **Grupo de Recursos**.  
2. Selecione a VM e discos associados.  
3. Clique em **Excluir**.  

---

## **📚 Recursos Úteis**  
🔹 [Documentação Oficial de VMs Azure](https://docs.microsoft.com/azure/virtual-machines/)  
🔹 [Tutoriais Azure VM](https://learn.microsoft.com/azure/virtual-machines/windows/quick-create-portal)  
🔹 [Calculadora de Custos Azure](https://azure.microsoft.com/pricing/calculator/)  

---

