import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Voz da Cidade',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: LoginPage(),
    );
  }
}

// Tela de Login com fundo degradê
class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        width: double.infinity,
        height: double.infinity,
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Center(
          child: SingleChildScrollView(
            padding: const EdgeInsets.all(24.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                // Logo / Ícone
                Icon(
                  Icons.location_city,
                  size: 90,
                  color: Colors.white,
                ),
                SizedBox(height: 16),
                Text(
                  "Voz da Cidade",
                  style: TextStyle(
                    fontSize: 28,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                SizedBox(height: 32),

                // Campo Email
                TextField(
                  decoration: InputDecoration(
                    filled: true,
                    fillColor: Colors.white,
                    prefixIcon: Icon(Icons.email, color: Color(0xFF004675)),
                    labelText: 'Email',
                    labelStyle: TextStyle(color: Color(0xFF004675)),
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(30),
                    ),
                    contentPadding:
                        EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                  ),
                ),
                SizedBox(height: 16),

                // Campo Senha
                TextField(
                  obscureText: true,
                  decoration: InputDecoration(
                    filled: true,
                    fillColor: Colors.white,
                    prefixIcon: Icon(Icons.lock, color: Color(0xFF004675)),
                    labelText: 'Senha',
                    labelStyle: TextStyle(color: Color(0xFF004675)),
                    border: OutlineInputBorder(
                      borderRadius: BorderRadius.circular(30),
                    ),
                    contentPadding:
                        EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                  ),
                ),
                SizedBox(height: 24),

                // Botão Login
                SizedBox(
                  width: double.infinity,
                  child: ElevatedButton(
                    onPressed: () {
                      Navigator.pushReplacement(
                        context,
                        MaterialPageRoute<void>(
                            builder: (BuildContext context) => AppPrincipalPage()),
                      );
                    },
                    style: ElevatedButton.styleFrom(
                      backgroundColor: Colors.white,
                      foregroundColor: Color(0xFF004675),
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      padding: EdgeInsets.symmetric(vertical: 16),
                      elevation: 4,
                    ),
                    child: Text(
                      'ENTRAR',
                      style:
                          TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
                    ),
                  ),
                ),
                SizedBox(height: 16),

                // Links
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  children: [
                    TextButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute<void>(
                              builder: (BuildContext context) => CadastroPage()),
                        );
                      },
                      child: Text(
                        'Cadastrar',
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                    TextButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute<void>(
                              builder: (BuildContext context) => EsqueciSenhaPage()),
                        );
                      },
                      child: Text(
                        'Esqueci a Senha',
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                  ],
                )
              ],
            ),
          ),
        ),
      ),
    );
  }
}

// Tela de Cadastro com link para voltar ao Login
class CadastroPage extends StatefulWidget {
  @override
  _CadastroPageState createState() => _CadastroPageState();
}

class _CadastroPageState extends State<CadastroPage> {
  final _formKey = GlobalKey<FormState>();
  final _nomeController = TextEditingController();
  final _emailController = TextEditingController();
  final _senhaController = TextEditingController();

  String? _validateNome(String? value) {
    if (value == null || value.trim().isEmpty) {
      return 'Por favor, insira seu nome';
    }
    return null;
  }

  String? _validateEmail(String? value) {
    if (value == null || value.trim().isEmpty) {
      return 'Por favor, insira seu email';
    }
    final emailRegex = RegExp(r'^[^@]+@[^@]+\.[^@]+');
    if (!emailRegex.hasMatch(value)) {
      return 'Email inválido';
    }
    return null;
  }

  String? _validateSenha(String? value) {
    if (value == null || value.isEmpty) {
      return 'Por favor, insira uma senha';
    }
    if (value.length < 8) {
      return 'Senha deve ter pelo menos 8 caracteres';
    }
    if (!RegExp(r'[A-Z]').hasMatch(value)) {
      return 'Senha deve conter ao menos uma letra maiúscula';
    }
    if (!RegExp(r'[0-9]').hasMatch(value)) {
      return 'Senha deve conter ao menos um número';
    }
    if (!RegExp(r'[!@#\$&~]').hasMatch(value)) {
      return 'Senha deve conter ao menos um caractere especial (!@#\$&~)';
    }
    return null;
  }

  void _cadastrar() {
    if (_formKey.currentState!.validate()) {
      Navigator.pop(context); // volta para o login
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        width: double.infinity,
        height: double.infinity,
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Center(
          child: SingleChildScrollView(
            padding: const EdgeInsets.all(24.0),
            child: Form(
              key: _formKey,
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  // Título
                  Icon(Icons.person_add, size: 80, color: Colors.white),
                  SizedBox(height: 16),
                  Text(
                    "Criar Conta",
                    style: TextStyle(
                      fontSize: 26,
                      fontWeight: FontWeight.bold,
                      color: Colors.white,
                    ),
                  ),
                  SizedBox(height: 32),

                  // Campo Nome
                  TextFormField(
                    controller: _nomeController,
                    decoration: InputDecoration(
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: Icon(Icons.person, color: Color(0xFF004675)),
                      labelText: 'Nome',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateNome,
                  ),
                  SizedBox(height: 16),

                  // Campo Email
                  TextFormField(
                    controller: _emailController,
                    decoration: InputDecoration(
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: Icon(Icons.email, color: Color(0xFF004675)),
                      labelText: 'Email',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateEmail,
                  ),
                  SizedBox(height: 16),

                  // Campo Senha
                  TextFormField(
                    controller: _senhaController,
                    obscureText: true,
                    decoration: InputDecoration(
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: Icon(Icons.lock, color: Color(0xFF004675)),
                      labelText: 'Senha',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateSenha,
                  ),
                  SizedBox(height: 8),

                  // Dica da senha
                  Row(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      Icon(Icons.info, size: 16, color: Colors.white),
                      SizedBox(width: 6),
                      Expanded(
                        child: Text(
                          'Senha deve ter pelo menos 8 caracteres, uma letra maiúscula, um número e um caractere especial (!@#\$&~).',
                          style:
                              TextStyle(color: Colors.white, fontSize: 12),
                        ),
                      ),
                    ],
                  ),

                  SizedBox(height: 24),

                  // Botão Cadastrar
                  SizedBox(
                    width: double.infinity,
                    child: ElevatedButton(
                      onPressed: _cadastrar,
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.white,
                        foregroundColor: Color(0xFF004675),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(30),
                        ),
                        padding: EdgeInsets.symmetric(vertical: 16),
                        elevation: 4,
                      ),
                      child: Text(
                        'CADASTRAR',
                        style: TextStyle(
                            fontSize: 16, fontWeight: FontWeight.bold),
                      ),
                    ),
                  ),

                  SizedBox(height: 16),

                  // Link para voltar ao login
                  TextButton(
                    onPressed: () {
                      Navigator.pop(context); // volta para o login
                    },
                    child: Text(
                      "Já tem conta? Entrar",
                      style: TextStyle(
                        color: Colors.white,
                        fontSize: 14,
                        decoration: TextDecoration.underline,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}

// Tela de Esqueci a Senha estilizada
class EsqueciSenhaPage extends StatefulWidget {
  @override
  _EsqueciSenhaPageState createState() => _EsqueciSenhaPageState();
}

class _EsqueciSenhaPageState extends State<EsqueciSenhaPage> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  bool _isEmailValido = false;

  String? _validateEmail(String? value) {
    if (value == null || value.trim().isEmpty) {
      return 'Por favor, insira seu email';
    }
    final emailRegex = RegExp(r'^[^@]+@[^@]+\.[^@]+');
    if (!emailRegex.hasMatch(value)) {
      return 'Email inválido';
    }
    return null;
  }

  void _onEmailChanged() {
    final isValid = _validateEmail(_emailController.text) == null;
    if (isValid != _isEmailValido) {
      setState(() {
        _isEmailValido = isValid;
      });
    }
  }

  void _enviarEmail() {
    if (_formKey.currentState!.validate()) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Email de recuperação enviado!')),
      );
      Navigator.pop(context);
    }
  }

  @override
  void initState() {
    super.initState();
    _emailController.addListener(_onEmailChanged);
  }

  @override
  void dispose() {
    _emailController.removeListener(_onEmailChanged);
    _emailController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        width: double.infinity,
        height: double.infinity,
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Center(
          child: SingleChildScrollView(
            padding: const EdgeInsets.all(24.0),
            child: Form(
              key: _formKey,
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Icon(Icons.lock_reset, size: 80, color: Colors.white),
                  SizedBox(height: 16),
                  Text(
                    "Recuperar Senha",
                    style: TextStyle(
                      fontSize: 26,
                      fontWeight: FontWeight.bold,
                      color: Colors.white,
                    ),
                  ),
                  SizedBox(height: 32),

                  // Campo Email
                  TextFormField(
                    controller: _emailController,
                    decoration: InputDecoration(
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: Icon(Icons.email, color: Color(0xFF004675)),
                      labelText: 'Email',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateEmail,
                    keyboardType: TextInputType.emailAddress,
                    autovalidateMode: AutovalidateMode.onUserInteraction,
                  ),
                  SizedBox(height: 24),

                  // Botão Enviar
                  SizedBox(
                    width: double.infinity,
                    child: ElevatedButton(
                      onPressed: _isEmailValido ? _enviarEmail : null,
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.white,
                        foregroundColor: Color(0xFF004675),
                        padding: EdgeInsets.symmetric(vertical: 16),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(30),
                        ),
                        elevation: 4,
                      ),
                      child: Text(
                        'ENVIAR',
                        style: TextStyle(
                          fontSize: 16,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ),
                  ),

                  SizedBox(height: 16),

                  // Link voltar ao login
                  TextButton(
                    onPressed: () {
                      Navigator.pop(context);
                    },
                    child: Text(
                      "Voltar para o Login",
                      style: TextStyle(
                        color: Colors.white,
                        decoration: TextDecoration.underline,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}

// Modelos de dados
class Comentario {
  final String texto;
  final DateTime dataHora;
  Comentario({required this.texto, required this.dataHora});
}

class Ocorrencia {
  final String titulo;
  final String descricao;
  final DateTime dataHora;
  final String categoria;
  final String localizacao;
  final List<Comentario> comentarios;
  String status;

  Ocorrencia({
    required this.titulo,
    required this.descricao,
    required this.dataHora,
    required this.categoria,
    required this.localizacao,
    required this.comentarios,
    required this.status,
  });
}

class Notificacao {
  final String titulo;
  final String mensagem;
  final DateTime dataHora;
  Notificacao({required this.titulo, required this.mensagem, required this.dataHora});
}

// Tela Principal Refatorada
class AppPrincipalPage extends StatefulWidget {
  const AppPrincipalPage({Key? key}) : super(key: key);

  @override
  _AppPrincipalPageState createState() => _AppPrincipalPageState();
}

class _AppPrincipalPageState extends State<AppPrincipalPage> {
  int _selectedIndex = 0;
  List<Ocorrencia> _ocorrencias = <Ocorrencia>[
    Ocorrencia(
      titulo: 'Buraco na rua',
      descricao: 'Há um buraco na rua principal.',
      dataHora: DateTime.now(),
      categoria: 'Infraestrutura',
      localizacao: 'Rua Principal',
      comentarios: <Comentario>[Comentario(texto: 'É verdade!', dataHora: DateTime.now())],
      status: 'Aberto',
    ),
    Ocorrencia(
      titulo: 'Falta de iluminação',
      descricao: 'A rua está escura à noite.',
      dataHora: DateTime.now(),
      categoria: 'Iluminação',
      localizacao: 'Rua X',
      comentarios: <Comentario>[],
      status: 'Em andamento',
    ),
  ];

  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Voz da Cidade'),
        backgroundColor: Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: _getPage(_selectedIndex),
      ),
      bottomNavigationBar: Container(
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.vertical(top: Radius.circular(20)),
          boxShadow: <BoxShadow>[BoxShadow(color: Colors.black26, blurRadius: 10, spreadRadius: 1)],
        ),
        child: BottomNavigationBar(
          currentIndex: _selectedIndex,
          onTap: _onItemTapped,
          selectedItemColor: Color(0xFF004675),
          unselectedItemColor: Colors.grey,
          showUnselectedLabels: true,
          items: const <BottomNavigationBarItem>[
            BottomNavigationBarItem(icon: Icon(Icons.home, size: 28), label: 'Home'),
            BottomNavigationBarItem(icon: Icon(Icons.event_note, size: 28), label: 'Eventos'),
            BottomNavigationBarItem(icon: Icon(Icons.add_box, size: 28), label: 'Nova Ocorrência'),
            BottomNavigationBarItem(icon: Icon(Icons.group, size: 28), label: 'Comunidade'),
            BottomNavigationBarItem(icon: Icon(Icons.list_alt, size: 28), label: 'Ocorrências'),
            BottomNavigationBarItem(icon: Icon(Icons.person, size: 28), label: 'Perfil'),
          ],
        ),
      ),
    );
  }

  Widget _getPage(int index) {
    switch (index) {
      case 0:
        return HomePageContent();
      case 1:
        return EventosPageContent();
      case 2:
        return NovaOcorrenciaPage(
          onOcorrenciaEnviada: (Ocorrencia ocorrencia) {
            setState(() {
              _ocorrencias.add(ocorrencia);
            });
          },
        );
      case 3:
        return MuralComunidade();
      case 4:
        return VisualizarOcorrenciasPage(ocorrencias: _ocorrencias);
      case 5:
        return PerfilUsuarioPage(
          nome: 'Nome do Usuário',
          email: 'email@exemplo.com',
          onSalvar: (String nome, String email) {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(content: Text('Perfil de $nome atualizado para $email!')),
            );
          },
        );
      default:
        return HomePageContent();
    }
  }
}

// Conteúdo da HomePage com Cards Modernos
class HomePageContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(16.0),
      child: ListView(
        children: <Widget>[
          _buildCard(
            context,
            'Notícias da Cidade',
            'Fique por dentro das últimas notícias e eventos.',
            Icons.article,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => NoticiasPage())),
          ),
          _buildCard(
            context,
            'Eventos',
            'Veja os próximos eventos na cidade.',
            Icons.event,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => EventosPageContent())),
          ),
          _buildCard(
            context,
            'Dicas de Segurança',
            'Dicas para manter sua segurança e bem-estar.',
            Icons.security,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => DicasSegurancaPage())),
          ),
          _buildCard(
            context,
            'Serviços Públicos',
            'Informações sobre serviços disponíveis na cidade.',
            Icons.public,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => ServicosPublicosPage())),
          ),
        ],
      ),
    );
  }

  Widget _buildCard(BuildContext context, String title, String subtitle, IconData icon, VoidCallback onTap) {
    return Card(
      margin: EdgeInsets.symmetric(vertical: 8),
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
      elevation: 4,
      child: ListTile(
        leading: Icon(icon, color: Color(0xFF004675)),
        title: Text(title, style: TextStyle(fontWeight: FontWeight.bold)),
        subtitle: Text(subtitle),
        trailing: Icon(Icons.arrow_forward),
        onTap: onTap,
      ),
    );
  }
}

// Tela de Eventos Refatorada
class EventosPageContent extends StatelessWidget {
  const EventosPageContent({Key? key}) : super(key: key);

  final List<Map<String, String>> eventos = const <Map<String, String>>[
    {
      'titulo': 'Feira Cultural',
      'descricao': 'Venha conhecer artes e comidas típicas da cidade.',
      'data': '10/09/2025'
    },
    {
      'titulo': 'Show de Música',
      'descricao': 'Apresentação ao vivo no centro da cidade.',
      'data': '15/09/2025'
    },
    {
      'titulo': 'Aula de Yoga ao Ar Livre',
      'descricao': 'Traga seu tapete e aproveite uma manhã saudável.',
      'data': '20/09/2025'
    },
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Eventos da Cidade'),
        backgroundColor: Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: ListView.builder(
          padding: EdgeInsets.all(16),
          itemCount: eventos.length,
          itemBuilder: (BuildContext context, int index) {
            final Map<String, String> evento = eventos[index];
            return Card(
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(16),
              ),
              elevation: 4,
              margin: EdgeInsets.symmetric(vertical: 8),
              child: ListTile(
                contentPadding: EdgeInsets.all(16),
                leading: Icon(Icons.event, color: Color(0xFF004675), size: 36),
                title: Text(evento['titulo']!, style: TextStyle(fontWeight: FontWeight.bold)),
                subtitle: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: <Widget>[
                    SizedBox(height: 4),
                    Text(evento['descricao']!),
                    SizedBox(height: 4),
                    Text('Data: ${evento['data']!}', style: TextStyle(fontSize: 12, color: Colors.grey[700])),
                  ],
                ),
                trailing: Icon(Icons.arrow_forward),
                onTap: () {
                  ScaffoldMessenger.of(context).showSnackBar(
                    SnackBar(content: Text('Mais informações sobre "${evento['titulo']!}"')),
                  );
                },
              ),
            );
          },
        ),
      ),
    );
  }
}

// Tela de Nova Ocorrência Refatorada
class NovaOcorrenciaPage extends StatefulWidget {
  final Function(Ocorrencia) onOcorrenciaEnviada;

  NovaOcorrenciaPage({Key? key, required this.onOcorrenciaEnviada}) : super(key: key);

  @override
  _NovaOcorrenciaPageState createState() => _NovaOcorrenciaPageState();
}

class _NovaOcorrenciaPageState extends State<NovaOcorrenciaPage> {
  final _formKey = GlobalKey<FormState>();
  String? _titulo;
  String? _descricao;
  String? _categoria;
  String? _localizacao;

  void _enviarOcorrencia() {
    if (_formKey.currentState!.validate()) {
      _formKey.currentState!.save();
      final Ocorrencia newOcorrencia = Ocorrencia(
        titulo: _titulo!,
        descricao: _descricao!,
        dataHora: DateTime.now(),
        categoria: _categoria!,
        localizacao: _localizacao!,
        comentarios: <Comentario>[],
        status: 'Aberto',
      );
      widget.onOcorrenciaEnviada(newOcorrencia);
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Ocorrência enviada com sucesso!')),
      );
      // Volta para a tela principal
      Navigator.pop(context);
    }
  }

  Widget _buildTextField({
    required String label,
    required IconData icon,
    int? maxLines = 1,
    required void Function(String?) onSaved,
    required String? Function(String?) validator,
  }) {
    return TextFormField(
      decoration: InputDecoration(
        filled: true,
        fillColor: Colors.white,
        prefixIcon: Icon(icon, color: Color(0xFF004675)),
        labelText: label,
        border: OutlineInputBorder(
          borderRadius: BorderRadius.circular(16),
        ),
      ),
      maxLines: maxLines,
      onSaved: onSaved,
      validator: validator,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Nova Ocorrência'),
        backgroundColor: Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: SingleChildScrollView(
          padding: EdgeInsets.all(16),
          child: Form(
            key: _formKey,
            child: Column(
              children: <Widget>[
                _buildTextField(
                  label: 'Título',
                  icon: Icons.short_text,
                  onSaved: (String? value) => _titulo = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira um título' : null,
                ),
                SizedBox(height: 16),
                _buildTextField(
                  label: 'Descrição',
                  icon: Icons.description,
                  maxLines: 3,
                  onSaved: (String? value) => _descricao = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira uma descrição' : null,
                ),
                SizedBox(height: 16),
                _buildTextField(
                  label: 'Categoria',
                  icon: Icons.category,
                  onSaved: (String? value) => _categoria = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira uma categoria' : null,
                ),
                SizedBox(height: 16),
                _buildTextField(
                  label: 'Localização',
                  icon: Icons.location_on,
                  onSaved: (String? value) => _localizacao = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira uma localização' : null,
                ),
                SizedBox(height: 24),
                SizedBox(
                  width: double.infinity,
                  child: ElevatedButton(
                    onPressed: _enviarOcorrencia,
                    style: ElevatedButton.styleFrom(
                      backgroundColor: Colors.white,
                      foregroundColor: Color(0xFF004675),
                      padding: EdgeInsets.symmetric(vertical: 16),
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      elevation: 4,
                    ),
                    child: Text(
                      'ENVIAR OCORRÊNCIA',
                      style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
                    ),
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

class DicasSegurancaPage extends StatelessWidget {
  const DicasSegurancaPage({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Dicas de Segurança'), backgroundColor: Color(0xFF004675), foregroundColor: Colors.white),
      body: Center(child: Text('Conteúdo das Dicas de Segurança')),
    );
  }
}

class ServicosPublicosPage extends StatelessWidget {
  const ServicosPublicosPage({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Serviços Públicos'), backgroundColor: Color(0xFF004675), foregroundColor: Colors.white),
      body: Center(child: Text('Conteúdo dos Serviços Públicos')),
    );
  }
}

class NoticiasPage extends StatelessWidget {
  const NoticiasPage({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Notícias da Cidade'), backgroundColor: Color(0xFF004675), foregroundColor: Colors.white),
      body: Center(child: Text('Conteúdo das Notícias')),
    );
  }
}

class VisualizarOcorrenciasPage extends StatelessWidget {
  final List<Ocorrencia> ocorrencias;

  const VisualizarOcorrenciasPage({Key? key, required this.ocorrencias}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Minhas Ocorrências'),
        backgroundColor: Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: ocorrencias.isEmpty
          ? Center(child: Text('Nenhuma ocorrência registrada.'))
          : ListView.builder(
              itemCount: ocorrencias.length,
              itemBuilder: (BuildContext context, int index) {
                final Ocorrencia ocorrencia = ocorrencias[index];
                return Card(
                  margin: EdgeInsets.all(8),
                  child: ListTile(
                    title: Text(ocorrencia.titulo),
                    subtitle: Text('${ocorrencia.descricao} - ${ocorrencia.status}'),
                  ),
                );
              },
            ),
    );
  }
}

class PerfilUsuarioPage extends StatefulWidget {
  final String nome;
  final String email;
  final Function(String, String) onSalvar;

  PerfilUsuarioPage({Key? key, required this.nome, required this.email, required this.onSalvar}) : super(key: key);

  @override
  _PerfilUsuarioPageState createState() => _PerfilUsuarioPageState();
}

class _PerfilUsuarioPageState extends State<PerfilUsuarioPage> {
  late TextEditingController _nomeController;
  late TextEditingController _emailController;

  @override
  void initState() {
    super.initState();
    _nomeController = TextEditingController(text: widget.nome);
    _emailController = TextEditingController(text: widget.email);
  }

  @override
  void dispose() {
    _nomeController.dispose();
    _emailController.dispose();
    super.dispose();
  }

  void _salvar() {
    widget.onSalvar(_nomeController.text, _emailController.text);
    Navigator.pop(context); //volta para a tela anterior
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Perfil do Usuário'),
        backgroundColor: Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: <Widget>[
            TextField(
              controller: _nomeController,
              decoration: InputDecoration(labelText: 'Nome'),
            ),
            TextField(
              controller: _emailController,
              decoration: InputDecoration(labelText: 'Email'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _salvar,
              child: Text('Salvar Alterações'),
            ),
          ],
        ),
      ),
    );
  }
}

// Classe de dados para um post (agora com likes e comentários)
class PostComunidade {
  final String titulo;
  final String conteudo;
  final String autor;
  final int timestamp;
  int likes;
  List<String> comentarios;

  PostComunidade({
    required this.titulo,
    required this.conteudo,
    required this.autor,
    required this.timestamp,
    this.likes = 0,
    this.comentarios = const [],
  });
}

// Widget do Mural da Comunidade - StatefulWidget
class MuralComunidade extends StatefulWidget {
  const MuralComunidade({Key? key}) : super(key: key);

  @override
  _MuralComunidadeState createState() => _MuralComunidadeState();
}

class _MuralComunidadeState extends State<MuralComunidade> {
  // Dados fictícios para demonstração
  final List<PostComunidade> _posts = [
    PostComunidade(
      titulo: 'Evento de Limpeza do Bairro',
      conteudo: 'Vamos nos reunir no sábado para limpar o parque central. Traga sua luva e saco de lixo!',
      autor: 'Maria Silva',
      timestamp: 1757308800,
      likes: 15,
      comentarios: ['Ótima iniciativa!', 'Estarei lá!'],
    ),
    PostComunidade(
      titulo: 'Doação de Agasalhos',
      conteudo: 'Estamos arrecadando agasalhos para ajudar famílias em situação de vulnerabilidade. Pontos de coleta: Praça Municipal e Sede da Associação de Moradores.',
      autor: 'João Pereira',
      timestamp: 1757049600,
      likes: 8,
      comentarios: ['Posso ajudar com a coleta?', 'Excelente trabalho!'],
    ),
  ];

  final TextEditingController _postTextController = TextEditingController();

  void _addPost() {
    if (_postTextController.text.isNotEmpty) {
      final newPost = PostComunidade(
        titulo: 'Nova Publicação', // Você pode expandir para que o usuário defina o título
        conteudo: _postTextController.text,
        autor: 'Usuário Atual', // Substitua por dados do usuário logado
        timestamp: DateTime.now().millisecondsSinceEpoch ~/ 1000,
      );
      setState(() {
        _posts.insert(0, newPost);
      });
      _postTextController.clear();
    }
  }

  void _toggleLike(int index) {
    setState(() {
      _posts[index].likes++;
    });
  }

  void _showCommentsModal(int index) {
    final post = _posts[index];
    final TextEditingController commentController = TextEditingController();

    showModalBottomSheet(
      context: context,
      isScrollControlled: true,
      builder: (BuildContext context) {
        return Padding(
          padding: EdgeInsets.only(
            bottom: MediaQuery.of(context).viewInsets.bottom,
          ),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              Container(
                width: double.infinity,
                padding: const EdgeInsets.all(16.0),
                decoration: const BoxDecoration(
                  color: Color(0xFF004675),
                  borderRadius: BorderRadius.vertical(top: Radius.circular(16)),
                ),
                child: const Text(
                  'Comentários',
                  style: TextStyle(
                    fontSize: 20,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                  textAlign: TextAlign.center,
                ),
              ),
              Expanded(
                child: ListView.builder(
                  shrinkWrap: true,
                  itemCount: post.comentarios.length,
                  itemBuilder: (context, commentIndex) {
                    return ListTile(
                      title: Text(post.comentarios[commentIndex]),
                      // Adicione mais detalhes aqui, como nome do autor do comentário, etc.
                    );
                  },
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(8.0),
                child: Row(
                  children: [
                    Expanded(
                      child: TextField(
                        controller: commentController,
                        decoration: InputDecoration(
                          hintText: 'Adicione um comentário...',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(20),
                          ),
                          contentPadding: const EdgeInsets.symmetric(horizontal: 20),
                        ),
                      ),
                    ),
                    const SizedBox(width: 8),
                    IconButton(
                      icon: const Icon(Icons.send),
                      color: const Color(0xFF004675),
                      onPressed: () {
                        if (commentController.text.isNotEmpty) {
                          setState(() {
                            post.comentarios.add(commentController.text);
                          });
                          commentController.clear();
                          // Fecha o teclado
                          FocusScope.of(context).unfocus();
                        }
                      },
                    ),
                  ],
                ),
              ),
            ],
          ),
        );
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Mural da Comunidade'),
        backgroundColor: const Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: [Color(0xFF004675), Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Column(
          children: [
            Expanded(
              child: ListView.builder(
                padding: const EdgeInsets.all(16),
                itemCount: _posts.length,
                itemBuilder: (BuildContext context, int index) {
                  final post = _posts[index];
                  final DateTime postDate = DateTime.fromMillisecondsSinceEpoch(post.timestamp * 1000);
                  return Card(
                    shape: RoundedRectangleBorder(
                      borderRadius: BorderRadius.circular(16),
                    ),
                    elevation: 4,
                    margin: const EdgeInsets.symmetric(vertical: 8),
                    child: Padding(
                      padding: const EdgeInsets.all(16.0),
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            post.titulo,
                            style: const TextStyle(
                              fontSize: 18,
                              fontWeight: FontWeight.bold,
                              color: Color(0xFF004675),
                            ),
                          ),
                          const SizedBox(height: 8),
                          Text(
                            post.conteudo,
                            style: const TextStyle(fontSize: 14),
                          ),
                          const SizedBox(height: 12),
                          Row(
                            children: [
                              const Icon(Icons.person, size: 16, color: Colors.grey),
                              const SizedBox(width: 4),
                              Text(
                                post.autor,
                                style: const TextStyle(fontSize: 12, fontStyle: FontStyle.italic),
                              ),
                              const Spacer(),
                              const Icon(Icons.access_time, size: 16, color: Colors.grey),
                              const SizedBox(width: 4),
                              Text(
                                '${postDate.day}/${postDate.month}/${postDate.year}',
                                style: TextStyle(fontSize: 12, color: Colors.grey[700]),
                              ),
                            ],
                          ),
                          const Divider(),
                          Row(
                            mainAxisAlignment: MainAxisAlignment.spaceAround,
                            children: [
                              GestureDetector(
                                onTap: () => _toggleLike(index),
                                child: Row(
                                  children: [
                                    Icon(Icons.thumb_up, color: post.likes > 0 ? Colors.blue : Colors.grey),
                                    const SizedBox(width: 4),
                                    Text('${post.likes}'),
                                  ],
                                ),
                              ),
                              GestureDetector(
                                onTap: () => _showCommentsModal(index),
                                child: Row(
                                  children: [
                                    const Icon(Icons.comment, color: Colors.grey),
                                    const SizedBox(width: 4),
                                    Text('${post.comentarios.length}'),
                                  ],
                                ),
                              ),
                            ],
                          ),
                        ],
                      ),
                    ),
                  );
                },
              ),
            ),
            // Área de criação de posts
            Padding(
              padding: const EdgeInsets.all(16.0),
              child: Row(
                children: [
                  Expanded(
                    child: TextField(
                      controller: _postTextController,
                      decoration: InputDecoration(
                        hintText: 'O que você está pensando?',
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(20),
                        ),
                        contentPadding: const EdgeInsets.symmetric(horizontal: 20),
                      ),
                    ),
                  ),
                  const SizedBox(width: 8),
                  FloatingActionButton(
                    onPressed: _addPost,
                    backgroundColor: const Color(0xFF004675),
                    child: const Icon(Icons.send, color: Colors.white),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
