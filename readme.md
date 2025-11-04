# 🚀 Guia Rápido de Golang para Iniciantes

## 📋 Índice
- [Instalação](#instalação)
- [Comandos Básicos](#comandos-básicos)
- [Estrutura de Projeto](#estrutura-de-projeto)
- [Sintaxe Básica](#sintaxe-básica)
- [Funções e Métodos](#funções-e-métodos)
- [Gerenciamento de Dependências](#gerenciamento-de-dependências)
- [Build e Execução](#build-e-execução)
- [Exemplo Prático](#exemplo-prático)

## 🔧 Instalação
```bash
# Download e instalação pelo site oficial
# https://golang.org/dl/

# Verificar instalação
go version
```

## ⚡ Comandos Básicos

### Comandos Essenciais
```bash
# Executar arquivo Go
go run main.go

# Compilar para executável
go build

# Compilar e instalar
go install

# Baixar dependências
go mod download

# Limpar cache de módulos
go clean -modcache

# Formatar código
go fmt ./...

# Verificar erros
go vet

# Executar testes
go test
```

### Comandos de Módulos
```bash
# Inicializar módulo
go mod init nome-do-projeto

# Adicionar dependência
go get github.com/exemplo/pacote

# Remover dependências não utilizadas
go mod tidy

# Verificar dependências
go mod verify

# Ver todas as dependências
go list -m all
```

## 📁 Estrutura de Projeto
```
meu-projeto/
├── go.mod          # Arquivo de módulo
├── go.sum          # Checksums das dependências
├── main.go         # Arquivo principal
├── pkg/            # Pacotes reutilizáveis
├── cmd/            # Aplicações principais
├── internal/       # Código privado
└── README.md
```

## 🔤 Sintaxe Básica

### Declaração de Variáveis
```go
// Declaração explícita
var nome string = "João"
var idade int = 25

// Declaração implícita
nome := "João"
idade := 25

// Múltiplas declarações
var (
    nome   string = "João"
    idade  int    = 25
    ativo  bool   = true
)
```

### Tipos de Dados
```go
// Tipos básicos
var texto string = "Hello"
var numero int = 42
var decimal float64 = 3.14
var ativo bool = true

// Arrays e Slices
var array [5]int = [5]int{1, 2, 3, 4, 5}
var slice []int = []int{1, 2, 3}

// Maps
var mapa map[string]int = make(map[string]int)
mapa["idade"] = 25

// Structs
type Pessoa struct {
    Nome  string
    Idade int
}
```

### Estruturas de Controle
```go
// If/Else
if idade >= 18 {
    fmt.Println("Maior de idade")
} else {
    fmt.Println("Menor de idade")
}

// For Loop
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

// While (não existe, usa for)
for condicao {
    // código
}

// Switch
switch dia := time.Now().Weekday(); dia {
case time.Saturday, time.Sunday:
    fmt.Println("Fim de semana")
default:
    fmt.Println("Dia útil")
}
```

## 🎯 Funções e Métodos

### Sintaxe de Funções
```go
// Função básica
func nomeDaFuncao(parametro1 tipo1, parametro2 tipo2) tipoRetorno {
    return valor
}

// Exemplo prático
func somar(a int, b int) int {
    return a + b
}

// Múltiplos retornos
func dividir(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("divisão por zero")
    }
    return a / b, nil
}

// Função sem retorno
func exibirMensagem(msg string) {
    fmt.Println(msg)
}
```

### Métodos (Funções com Receiver)
```go
// Definindo um tipo
type Pessoa struct {
    Nome  string
    Idade int
}

// Método com receiver
func (p Pessoa) Apresentar() string {
    return fmt.Sprintf("Olá, eu sou %s e tenho %d anos", p.Nome, p.Idade)
}

// Método que modifica o receiver (pointer)
func (p *Pessoa) Aniversario() {
    p.Idade++
}

// Uso dos métodos
func main() {
    pessoa := Pessoa{Nome: "João", Idade: 25}
    fmt.Println(pessoa.Apresentar())
    
    pessoa.Aniversario()
    fmt.Println(pessoa.Idade) // 26
}
```

### Assinaturas e Parâmetros
```go
// Parâmetros do mesmo tipo
func calcular(a, b, c int) int {
    return a + b + c
}

// Parâmetros variádicos
func somarTodos(numeros ...int) int {
    total := 0
    for _, num := range numeros {
        total += num
    }
    return total
}

// Função como parâmetro
func executar(f func(int) int, valor int) int {
    return f(valor)
}

// Função anônima
quadrado := func(x int) int {
    return x * x
}
```

## 📦 Gerenciamento de Dependências

### go.mod (Arquivo de Módulo)
```go
module meu-projeto

go 1.21

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/gorilla/mux v1.8.0
)

replace github.com/exemplo/antigo => github.com/exemplo/novo v1.0.0
```

### Comandos de Dependências
```bash
# Adicionar dependência específica
go get github.com/gin-gonic/gin@v1.9.1

# Adicionar dependência mais recente
go get github.com/gorilla/mux@latest

# Remover dependência
go mod edit -droprequire github.com/exemplo/pacote

# Atualizar dependências
go get -u ./...
```

## 🏗️ Build e Execução

### Comandos de Build
```bash
# Build simples
go build

# Build com nome específico
go build -o meu-app

# Build para diferentes plataformas
GOOS=linux GOARCH=amd64 go build -o app-linux
GOOS=windows GOARCH=amd64 go build -o app.exe
GOOS=darwin GOARCH=amd64 go build -o app-mac

# Build otimizado (menor tamanho)
go build -ldflags="-s -w" -o app
```

### Execução
```bash
# Executar diretamente
go run main.go

# Executar com argumentos
go run main.go arg1 arg2

# Executar executável compilado
./meu-app
```

## 💡 Exemplo Prático

### main.go
```go
package main

import (
    "fmt"
    "os"
)

// Struct para representar uma pessoa
type Pessoa struct {
    Nome  string
    Idade int
    Email string
}

// Método para apresentação
func (p Pessoa) Apresentar() string {
    return fmt.Sprintf("Nome: %s, Idade: %d, Email: %s", p.Nome, p.Idade, p.Email)
}

// Método para verificar se é maior de idade
func (p Pessoa) MaiorIdade() bool {
    return p.Idade >= 18
}

// Função para criar nova pessoa
func NovaPessoa(nome string, idade int, email string) *Pessoa {
    return &Pessoa{
        Nome:  nome,
        Idade: idade,
        Email: email,
    }
}

// Função principal
func main() {
    // Verificar argumentos da linha de comando
    if len(os.Args) < 2 {
        fmt.Println("Uso: go run main.go [nome]")
        return
    }

    nome := os.Args[1]
    
    // Criar nova pessoa
    pessoa := NovaPessoa(nome, 25, nome+"@email.com")
    
    // Exibir informações
    fmt.Println("=== Informações da Pessoa ===")
    fmt.Println(pessoa.Apresentar())
    
    if pessoa.MaiorIdade() {
        fmt.Println("✅ Maior de idade")
    } else {
        fmt.Println("❌ Menor de idade")
    }
    
    // Exemplo com slice
    idades := []int{18, 25, 30, 16, 45}
    fmt.Printf("\nIdades: %v\n", idades)
    fmt.Printf("Média de idades: %.2f\n", calcularMedia(idades))
}

// Função para calcular média
func calcularMedia(numeros []int) float64 {
    if len(numeros) == 0 {
        return 0
    }
    
    soma := 0
    for _, num := range numeros {
        soma += num
    }
    
    return float64(soma) / float64(len(numeros))
}
```

### go.mod
```go
module exemplo-golang

go 1.21
```

## 🚀 Como Usar Este Exemplo

```bash
# 1. Criar pasta do projeto
mkdir meu-primeiro-go
cd meu-primeiro-go

# 2. Inicializar módulo
go mod init meu-primeiro-go

# 3. Criar arquivo main.go (copiar código acima)

# 4. Executar
go run main.go João

# 5. Compilar
go build -o app

# 6. Executar compilado
./app Maria
```

## 📚 Recursos Úteis

- **Documentação Oficial**: https://golang.org/doc/
- **Go by Example**: https://gobyexample.com/
- **Tour de Go**: https://tour.golang.org/
- **Go Playground**: https://play.golang.org/

## 🎯 Próximos Passos

1. **Aprenda sobre goroutines e channels** (concorrência)
2. **Explore o ecossistema Go** (gin, echo, gorm, etc.)
3. **Pratique com projetos reais** (APIs, CLIs, microservices)
4. **Entenda testing em Go** (`go test`)
5. **Aprenda sobre interfaces** (polimorfismo em Go)

---

**Dica**: 💡 Go é uma linguagem simples e poderosa. Pratique escrevendo código pequeno todos os dias!

**Happy Coding!** 🎉