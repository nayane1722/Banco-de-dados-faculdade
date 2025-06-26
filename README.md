-- Tabela de Empresas
CREATE TABLE Empresas (
    empresa_id INT PRIMARY KEY,
    nome VARCHAR(100),
    setor VARCHAR(50),
    porte VARCHAR(20),
    localizacao VARCHAR(100)
);

-- Tabela de Incidentes de Backup
CREATE TABLE Incidentes_Backup (
    incidente_id INT PRIMARY KEY,
    empresa_id INT,
    data_incidente DATE,
    tipo_falha VARCHAR(20), -- (hardware, humano, ransomware, software, configuração)
    impacto VARCHAR(10), -- (baixa, média, alta, crítica)
    tempo_indisponibilidade INT, -- em horas
    perdadedados VARCHAR(3), -- (sim/não)
    FOREIGN KEY (empresa_id) REFERENCES Empresas(empresa_id)
);

-- Tabela de Estratégias Atuais
CREATE TABLE Estratégias_Atuais (
    estrategia_id INT PRIMARY KEY,
    empresa_id INT,
    tipo_backup VARCHAR(20), -- (completo, incremental, diferencial)
    frequencia VARCHAR(50),
    armazenamento VARCHAR(20), -- (local, nuvem, híbrido, air-gapped)
    criptografado VARCHAR(3), -- (sim/não)
    possuitestesrestauracao VARCHAR(3), -- (sim/não)
    ferramentas_utilizadas TEXT,
    FOREIGN KEY (empresa_id) REFERENCES Empresas(empresa_id)
);

-- Tabela de Ações Corretivas
CREATE TABLE Ações_Corretivas (
    acao_id INT PRIMARY KEY,
    incidente_id INT,
    descricao_acao TEXT,
    data_execucao DATE,
    eficacia VARCHAR(20), -- (melhorou, permaneceu igual, piorou)
    FOREIGN KEY (incidente_id) REFERENCES Incidentes_Backup(incidente_id)
);

-- Tabela de Indicadores de Desempenho
CREATE TABLE Indicadores_Desempenho (
    indicador_id INT PRIMARY KEY,
    empresa_id INT,
    taxasucessorestauracao DECIMAL(5,2),
    tempomediorecuperacao DECIMAL(5,2),
    porcentagembackupvalido DECIMAL(5,2),
    frequencia_testes VARCHAR(50),
    FOREIGN KEY (empresa_id) REFERENCES Empresas(empresa_id)
);
