# Código do Servidor (Back-end)
const agora = new Date();

// Data de hoje no fuso de São Paulo no formato YYYY-MM-DD
const dataHoje = new Intl.DateTimeFormat('sv-SE', {
  timeZone: 'America/Sao_Paulo',
}).format(agora);

// Dia da semana de hoje no fuso de São Paulo
let diaSemanaHoje = agora.toLocaleDateString('pt-BR', {
  weekday: 'long',
  timeZone: 'America/Sao_Paulo',
}).toLowerCase();

diaSemanaHoje = diaSemanaHoje
  .replace('-feira', '')
  .normalize('NFD')
  .replace(/[\u0300-\u036f]/g, '');

// Função para normalizar texto
function normalizar(valor) {
  return String(valor || '')
    .trim()
    .toLowerCase()
    .normalize('NFD')
    .replace(/[\u0300-\u036f]/g, '');
}

return items.map(item => {
  const row = item.json;

  const ativo = normalizar(row.ATIVO).toUpperCase();
  const diaSemana = normalizar(row.DIA_SEMANA);
  const ultimoEnvio = String(row.ULTIMO_ENVIO || '').trim();

  const enviarHoje =
    ativo === 'SIM' &&
    diaSemana === diaSemanaHoje &&
    ultimoEnvio !== dataHoje;

  return {
    json: {
      ...row,
      data_hoje: dataHoje,
      dia_semana_hoje: diaSemanaHoje,
      enviar_hoje: enviarHoje,
    },
  };
});

const dias = ['domingo','segunda-feira','terça-feira','quarta-feira','quinta-feira','sextafeira','sábado'];
const hoje = dias[new Date().getDay()];
return items
 .filter(item => {
 const ativo = String(item.json.ATIVO || 'SIM').toUpperCase() === 'SIM';
 const dia = String(item.json.DIA_SEMANA || '').toLowerCase().trim();
 return ativo && dia === hoje;
 })
 .map(item => ({
 json: {
 ...item.json,
 deveEnviar: true,
 assunto: item.json.ASSUNTO,
 mensagem: item.json.MENSAGEM_HTML,
 destinatario: item.json.DESTINATARIO || 'destinatario@empresa.com'
 }
 })
## Organização

Organize os arquivos conforme o tipo de solução desenvolvida:

### Shell Scripts

Se a solução utiliza shell scripts, organize-os aqui com nomes descritivos:

```cmd
servidor/
├── scripts/
│   ├── configurar-firewall.sh
│   ├── monitorar-rede.sh
│   └── backup-configuracao.sh
└── README.md
```

### Back-end .NET / Outra Tecnologia

Se a solução utiliza uma API ou serviço back-end, organize conforme a estrutura padrão da tecnologia:

```cmd
servidor/
├── src/
│   └── (código-fonte)
├── tests/
│   └── (testes)
└── README.md
```

## Como Executar

*(Descreva aqui como executar o servidor localmente para desenvolvimento e testes.)*

## Variáveis de Ambiente

*(Liste as variáveis de ambiente necessárias, sem incluir valores reais de produção.)*

| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| *(Variável)* | *(Descrição)* | *(Exemplo)* |
