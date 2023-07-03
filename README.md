# PesquisaSOLID
1 - Mostre exemplos no código de todos os princípios de SOLID, são eles:
O SOLID é utilizado para que seja escrito um código mais limpo, separando responsabilidades , facilitando na refatoração e estimulando o reaproveitamento do código.
S — Single Responsibility (Responsabilidade Única)
// Classe para armazenar informações sobre o cliente
class Cliente {
    private String nome;
    private String email;
    private String telefone;
    public Cliente(String nome, String email, String telefone) {
        this.nome = nome;
        this.email = email;
        this.telefone = telefone;
    }
    // Getters e setters
    public String getNome() {
        return nome;
    }
    public void setNome(String nome) {
        this.nome = nome;
    }
    public String getEmail() {
        return email; }
    public void setEmail(String email) {
        this.email = email;
    }
    public String getTelefone() {
        return telefone;
    }
    public void setTelefone(String telefone) {
        this.telefone = telefone;
    }
}
// Classe responsável por exibir informações sobre o cliente
class ClientePrinter {
    public void imprimirDetalhesCliente(Cliente cliente) {
        System.out.println("Detalhes do cliente:");
        System.out.println("Nome: " + cliente.getNome());
        System.out.println("E-mail: " + cliente.getEmail());
        System.out.println("Telefone: " + cliente.getTelefone());
    }
}
O — Open-Closed (Aberto - Fechado):

// Classe base abstrata para formas geométricas
abstract class Forma {
    public abstract double calcularArea(); }
// Implementação de uma forma específica: Círculo
class Circulo extends Forma {
    private double raio;
    public Circulo(double raio) {
        this.raio = raio;
    }
    public double getRaio() {
        return raio;
    }
    public void setRaio(double raio) {
        this.raio = raio;
    }
    @Override
    public double calcularArea() {
        return Math.PI * raio * raio;
    }
}
// Implementação de outra forma específica: Retângulo
class Retangulo extends Forma {
    private double largura;
    private double altura;
    public Retangulo(double largura, double altura) {
        this.largura = largura;
        this.altura = altura; }
    public double getLargura() {
        return largura;
    }
    public void setLargura(double largura) {
        this.largura = largura;
    }
    public double getAltura() {
        return altura;
    }
    public void setAltura(double altura) {
        this.altura = altura;
    }
    @Override
    public double calcularArea() {
        return largura * altura;
    }
}
// Classe que utiliza as formas geométricas e calcula a área total
class CalculadoraArea {
    public double calcularAreaTotal(Forma[] formas) {
        double areaTotal = 0.0;
        for (Forma forma : formas) {
            areaTotal += forma.calcularArea();
        }
        return areaTotal; }
}
L — Liskov Substitution (Substituição de Liskov)
// Classe base abstrata para uma forma geométrica
abstract class Forma {
    public abstract double calcularArea();
}
// Implementação de uma forma específica: Retângulo
class Retangulo extends Forma {
    private double largura;
    private double altura;
    public Retangulo(double largura, double altura) {
        this.largura = largura;
        this.altura = altura;
    }
    public double getLargura() {
        return largura;
    }
    public void setLargura(double largura) {
        this.largura = largura;
    }
    public double getAltura() {
        return altura;
    }
    public void setAltura(double altura) {
        this.altura = altura;
    }
    @Override
    public double calcularArea() {
        return largura * altura;
    }
}
// Implementação de uma forma específica: Quadrado
class Quadrado extends Forma {
    private double lado;
    public Quadrado(double lado) {
        this.lado = lado;
    }
    public double getLado() {
        return lado;
    }
    public void setLado(double lado) {
        this.lado = lado;
    }
    @Override
    public double calcularArea() {
        return lado * lado;
    }
}
// Função genérica que recebe uma forma e imprime sua área
public void imprimirArea(Forma forma) {
    double area = forma.calcularArea();
    System.out.println("Área: " + area);
}
I — Interface Segregation (Segregação por Interface)
// Interface para uma impressora
interface Impressora {
    void imprimir();
}
// Interface para uma função de digitalização
interface Scanner {
    void digitalizar();
}
// Interface para uma máquina de fax
interface Fax {
    void enviarFax();
}
// Classe que implementa apenas a interface de impressora
class ImpressoraComum implements Impressora {
    @Override
    public void imprimir() {
        System.out.println("Imprimindo documento...");
    }
}
// Classe que implementa apenas a interface de scanner
class ScannerComum implements Scanner {
    @Override
    public void digitalizar() {
        System.out.println("Digitalizando documento...");
    }
}
// Classe que implementa apenas a interface de fax
class FaxComum implements Fax {
    @Override
    public void enviarFax() {
        System.out.println("Enviando fax...");
    }
}
// Classe que utiliza as interfaces de impressora e scanner
class ImpressoraScanner implements Impressora, Scanner {
    @Override
    public void imprimir() {
        System.out.println("Imprimindo documento...");
    }
    @Override
    public void digitalizar() {
        System.out.println("Digitalizando documento...");
    }
}
D — Dependency Inversion (Inversão de Dependência)

// Interface para um serviço de envio de mensagens
interface ServicoEnvioMensagem {
    void enviarMensagem(String mensagem);
}
// Implementação concreta do serviço de envio de mensagens via e-mail
class ServicoEnvioEmail implements ServicoEnvioMensagem {
    @Override
    public void enviarMensagem(String mensagem) {
        System.out.println("Enviando mensagem por e-mail: " + mensagem);
    }
}
// Implementação concreta do serviço de envio de mensagens via SMS
class ServicoEnvioSMS implements ServicoEnvioMensagem {
    @Override
    public void enviarMensagem(String mensagem) {
        System.out.println("Enviando mensagem por SMS: " + mensagem);
    }
}
// Classe de alto nível que depende de um serviço de envio de mensagens
class Notificador {
    private ServicoEnvioMensagem servicoEnvioMensagem;
    public Notificador(ServicoEnvioMensagem servicoEnvioMensagem) {
        this.servicoEnvioMensagem = servicoEnvioMensagem;
    }
    public void enviarNotificacao(String mensagem) {
        servicoEnvioMensagem.enviarMensagem(mensagem);
    }
}
