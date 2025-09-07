import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Voz da Cidade',
      debugShowCheckedModeBanner: false, // Remove a faixa de debug no canto
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
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
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
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
                const Icon(
                  Icons.location_city,
                  size: 90,
                  color: Colors.white,
                ),
                const SizedBox(height: 16),
                const Text(
                  "Voz da Cidade",
                  style: TextStyle(
                    fontSize: 28,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                const SizedBox(height: 32),

                // Campo Email
                const TextField(
                  decoration: const InputDecoration( // Added const here
                    filled: true,
                    fillColor: Colors.white,
                    prefixIcon: const Icon(Icons.email, color: const Color(0xFF004675)), // Added const to Icon and Color
                    labelText: 'Email',
                    labelStyle: const TextStyle(color: const Color(0xFF004675)), // Added const to TextStyle and Color
                    border: const OutlineInputBorder( // Added const here
                      borderRadius: const BorderRadius.all(Radius.circular(30.0)), // Fixed: Made BorderRadius const
                    ),
                    contentPadding:
                        const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                  ),
                ),
                const SizedBox(height: 16),

                // Campo Senha
                const TextField(
                  obscureText: true,
                  decoration: const InputDecoration( // Added const here
                    filled: true,
                    fillColor: Colors.white,
                    prefixIcon: const Icon(Icons.lock, color: const Color(0xFF004675)), // Added const to Icon and Color
                    labelText: 'Senha',
                    labelStyle: const TextStyle(color: const Color(0xFF004675)), // Added const to TextStyle and Color
                    border: const OutlineInputBorder( // Added const here
                      borderRadius: const BorderRadius.all(Radius.circular(30.0)), // Fixed: Made BorderRadius const
                    ),
                    contentPadding:
                        const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                  ),
                ),
                const SizedBox(height: 24),

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
                      foregroundColor: const Color(0xFF004675),
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      padding: const EdgeInsets.symmetric(vertical: 16),
                      elevation: 4,
                    ),
                    child: const Text(
                      'ENTRAR',
                      style:
                          TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
                    ),
                  ),
                ),
                const SizedBox(height: 16),

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
                      child: const Text(
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
                      child: const Text(
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
    final RegExp emailRegex = RegExp(r'^[^@]+@[^@]+\.[^@]+');
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
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
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
                  const Icon(Icons.person_add, size: 80, color: Colors.white),
                  const SizedBox(height: 16),
                  const Text(
                    "Criar Conta",
                    style: TextStyle(
                      fontSize: 26,
                      fontWeight: FontWeight.bold,
                      color: Colors.white,
                    ),
                  ),
                  const SizedBox(height: 32),

                  // Campo Nome
                  TextFormField(
                    controller: _nomeController,
                    decoration: const InputDecoration( // Added const here
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: const Icon(Icons.person, color: const Color(0xFF004675)), // Added const to Color
                      labelText: 'Nome',
                      border: const OutlineInputBorder( // Added const here
                        borderRadius: const BorderRadius.all(Radius.circular(30.0)), // Fixed: Made BorderRadius const
                      ),
                      contentPadding:
                          const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateNome,
                  ),
                  const SizedBox(height: 16),

                  // Campo Email
                  TextFormField(
                    controller: _emailController,
                    decoration: const InputDecoration( // Added const here
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: const Icon(Icons.email, color: const Color(0xFF004675)), // Added const to Color
                      labelText: 'Email',
                      border: const OutlineInputBorder( // Added const here
                        borderRadius: const BorderRadius.all(Radius.circular(30.0)), // Fixed: Made BorderRadius const
                      ),
                      contentPadding:
                          const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateEmail,
                  ),
                  const SizedBox(height: 16),

                  // Campo Senha
                  TextFormField(
                    controller: _senhaController,
                    obscureText: true,
                    decoration: const InputDecoration( // Added const here
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: const Icon(Icons.lock, color: const Color(0xFF004675)), // Added const to Color
                      labelText: 'Senha',
                      border: const OutlineInputBorder( // Added const here
                        borderRadius: const BorderRadius.all(Radius.circular(30.0)), // Fixed: Made BorderRadius const
                      ),
                      contentPadding:
                          const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateSenha,
                  ),
                  const SizedBox(height: 8),

                  // Dica da senha
                  const Row(
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

                  const SizedBox(height: 24),

                  // Botão Cadastrar
                  SizedBox(
                    width: double.infinity,
                    child: ElevatedButton(
                      onPressed: _cadastrar,
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.white,
                        foregroundColor: const Color(0xFF004675),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(30),
                        ),
                        padding: const EdgeInsets.symmetric(vertical: 16),
                        elevation: 4,
                      ),
                      child: const Text(
                        'CADASTRAR',
                        style: TextStyle(
                            fontSize: 16, fontWeight: FontWeight.bold),
                      ),
                    ),
                  ),

                  const SizedBox(height: 16),

                  // Link para voltar ao login
                  TextButton(
                    onPressed: () {
                      Navigator.pop(context); // volta para o login
                    },
                    child: const Text(
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
    final RegExp emailRegex = RegExp(r'^[^@]+@[^@]+\.[^@]+');
    if (!emailRegex.hasMatch(value)) {
      return 'Email inválido';
    }
    return null;
  }

  void _onEmailChanged() {
    final bool isValid = _validateEmail(_emailController.text) == null;
    if (isValid != _isEmailValido) {
      setState(() {
        _isEmailValido = isValid;
      });
    }
  }

  void _enviarEmail() {
    if (_formKey.currentState!.validate()) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Email de recuperação enviado!')),
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
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
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
                  const Icon(Icons.lock_reset, size: 80, color: Colors.white),
                  const SizedBox(height: 16),
                  const Text(
                    "Recuperar Senha",
                    style: TextStyle(
                      fontSize: 26,
                      fontWeight: FontWeight.bold,
                      color: Colors.white,
                    ),
                  ),
                  const SizedBox(height: 32),

                  // Campo Email
                  TextFormField(
                    controller: _emailController,
                    decoration: const InputDecoration( // Added const here
                      filled: true,
                      fillColor: Colors.white,
                      prefixIcon: const Icon(Icons.email, color: const Color(0xFF004675)), // Added const to Color
                      labelText: 'Email',
                      border: const OutlineInputBorder( // Added const here
                        borderRadius: const BorderRadius.all(Radius.circular(30.0)), // Fixed: Made BorderRadius const
                      ),
                      contentPadding:
                          const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
                    ),
                    validator: _validateEmail,
                    keyboardType: TextInputType.emailAddress,
                    autovalidateMode: AutovalidateMode.onUserInteraction,
                  ),
                  const SizedBox(height: 24),

                  // Botão Enviar
                  SizedBox(
                    width: double.infinity,
                    child: ElevatedButton(
                      onPressed: _isEmailValido ? _enviarEmail : null,
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.white,
                        foregroundColor: const Color(0xFF004675),
                        padding: const EdgeInsets.symmetric(vertical: 16),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(30),
                        ),
                        elevation: 4,
                      ),
                      child: const Text(
                        'ENVIAR',
                        style: TextStyle(
                          fontSize: 16,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ),
                  ),

                  const SizedBox(height: 16),

                  // Link voltar ao login
                  TextButton(
                    onPressed: () {
                      Navigator.pop(context);
                    },
                    child: const Text(
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
  final List<Ocorrencia> _ocorrencias = <Ocorrencia>[
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
        title: const Text('Voz da Cidade'),
        backgroundColor: const Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: _getPage(_selectedIndex),
      ),
      bottomNavigationBar: Container(
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: const BorderRadius.vertical(top: Radius.circular(20)),
          boxShadow: const <BoxShadow>[BoxShadow(color: Colors.black26, blurRadius: 10, spreadRadius: 1)], // Added const to the list
        ),
        child: BottomNavigationBar(
          currentIndex: _selectedIndex,
          onTap: _onItemTapped,
          selectedItemColor: const Color(0xFF004675),
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
        return const EventosPageContent();
      case 2:
        return NovaOcorrenciaPage(
          onOcorrenciaEnviada: (Ocorrencia ocorrencia) {
            setState(() {
              _ocorrencias.add(ocorrencia);
            });
          },
        );
      case 3:
        return const MuralComunidade();
      case 4:
        return VisualizarOcorrenciasPage(ocorrencias: _ocorrencias);
      case 5:
        return const PerfilUsuarioContentPage(); // Usando a versão mais rica do perfil
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
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => const NoticiasPage())),
          ),
          _buildCard(
            context,
            'Eventos',
            'Veja os próximos eventos na cidade.',
            Icons.event,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => const EventosPageContent())),
          ),
          _buildCard(
            context,
            'Dicas de Segurança',
            'Dicas para manter sua segurança e bem-estar.',
            Icons.security,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => const DicasSegurancaPage())),
          ),
          _buildCard(
            context,
            'Serviços Públicos',
            'Informações sobre serviços disponíveis na cidade.',
            Icons.public,
            () => Navigator.push<void>(context, MaterialPageRoute<void>(builder: (_) => const ServicosPublicosPage())),
          ),
        ],
      ),
    );
  }

  Widget _buildCard(BuildContext context, String title, String subtitle, IconData icon, VoidCallback onTap) {
    return Card(
      margin: const EdgeInsets.symmetric(vertical: 8),
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
      elevation: 4,
      child: ListTile(
        leading: Icon(icon, color: const Color(0xFF004675)),
        title: Text(title, style: const TextStyle(fontWeight: FontWeight.bold)),
        subtitle: Text(subtitle),
        trailing: const Icon(Icons.arrow_forward),
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
        title: const Text('Eventos da Cidade'),
        backgroundColor: const Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: ListView.builder(
          padding: const EdgeInsets.all(16),
          itemCount: eventos.length,
          itemBuilder: (BuildContext context, int index) {
            final Map<String, String> evento = eventos[index];
            return Card(
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(16),
              ),
              elevation: 4,
              margin: const EdgeInsets.symmetric(vertical: 8),
              child: ListTile(
                contentPadding: const EdgeInsets.all(16),
                leading: const Icon(Icons.event, color: Color(0xFF004675), size: 36),
                title: Text(evento['titulo']!, style: const TextStyle(fontWeight: FontWeight.bold)),
                subtitle: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: <Widget>[
                    const SizedBox(height: 4),
                    Text(evento['descricao']!),
                    const SizedBox(height: 4),
                    Text('Data: ${evento['data']!}', style: TextStyle(fontSize: 12, color: Colors.grey[700])),
                  ],
                ),
                trailing: const Icon(Icons.arrow_forward),
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

  const NovaOcorrenciaPage({Key? key, required this.onOcorrenciaEnviada}) : super(key: key);

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
        const SnackBar(content: Text('Ocorrência enviada com sucesso!')),
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
        prefixIcon: Icon(icon, color: const Color(0xFF004675)),
        labelText: label,
        border: const OutlineInputBorder( // Added const here
          borderRadius: const BorderRadius.all(Radius.circular(16.0)), // Fixed: Made BorderRadius const
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
        title: const Text('Nova Ocorrência'),
        backgroundColor: const Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16),
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
                const SizedBox(height: 16),
                _buildTextField(
                  label: 'Descrição',
                  icon: Icons.description,
                  maxLines: 3,
                  onSaved: (String? value) => _descricao = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira uma descrição' : null,
                ),
                const SizedBox(height: 16),
                _buildTextField(
                  label: 'Categoria',
                  icon: Icons.category,
                  onSaved: (String? value) => _categoria = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira uma categoria' : null,
                ),
                const SizedBox(height: 16),
                _buildTextField(
                  label: 'Localização',
                  icon: Icons.location_on,
                  onSaved: (String? value) => _localizacao = value,
                  validator: (String? value) => value!.isEmpty ? 'Insira uma localização' : null,
                ),
                const SizedBox(height: 24),
                SizedBox(
                  width: double.infinity,
                  child: ElevatedButton(
                    onPressed: _enviarOcorrencia,
                    style: ElevatedButton.styleFrom(
                      backgroundColor: Colors.white,
                      foregroundColor: const Color(0xFF004675),
                      padding: const EdgeInsets.symmetric(vertical: 16),
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(30),
                      ),
                      elevation: 4,
                    ),
                    child: const Text(
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
      appBar: AppBar(title: const Text('Dicas de Segurança'), backgroundColor: const Color(0xFF004675), foregroundColor: Colors.white),
      body: const Center(child: Text('Conteúdo das Dicas de Segurança')),
    );
  }
}

class ServicosPublicosPage extends StatelessWidget {
  const ServicosPublicosPage({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Serviços Públicos'), backgroundColor: const Color(0xFF004675), foregroundColor: Colors.white),
      body: const Center(child: Text('Conteúdo dos Serviços Públicos')),
    );
  }
}

class NoticiasPage extends StatelessWidget {
  const NoticiasPage({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Notícias da Cidade'), backgroundColor: const Color(0xFF004675), foregroundColor: Colors.white),
      body: const Center(child: Text('Conteúdo das Notícias')),
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
        title: const Text('Minhas Ocorrências'),
        backgroundColor: const Color(0xFF004675),
        foregroundColor: Colors.white,
      ),
      body: ocorrencias.isEmpty
          ? const Center(child: Text('Nenhuma ocorrência registrada.'))
          : ListView.builder(
              itemCount: ocorrencias.length,
              itemBuilder: (BuildContext context, int index) {
                final Ocorrencia ocorrencia = ocorrencias[index];
                return Card(
                  margin: const EdgeInsets.all(8),
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
      final PostComunidade newPost = PostComunidade(
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
    final PostComunidade post = _posts[index];
    final TextEditingController commentController = TextEditingController();

    showModalBottomSheet<void>(
      context: context,
      isScrollControlled: true,
      builder: (BuildContext context) {
        return Padding(
          padding: EdgeInsets.only(
            bottom: MediaQuery.of(context).viewInsets.bottom,
          ),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
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
                  itemBuilder: (BuildContext context, int commentIndex) {
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
                  children: <Widget>[
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
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Column(
          children: <Widget>[
            Expanded(
              child: ListView.builder(
                padding: const EdgeInsets.all(16),
                itemCount: _posts.length,
                itemBuilder: (BuildContext context, int index) {
                  final PostComunidade post = _posts[index];
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
                        children: <Widget>[
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
                            children: <Widget>[
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
                            children: <Widget>[
                              GestureDetector(
                                onTap: () => _toggleLike(index),
                                child: Row(
                                  children: <Widget>[
                                    Icon(Icons.thumb_up, color: post.likes > 0 ? Colors.blue : Colors.grey),
                                    const SizedBox(width: 4),
                                    Text('${post.likes}'),
                                  ],
                                ),
                              ),
                              GestureDetector(
                                onTap: () => _showCommentsModal(index),
                                child: Row(
                                  children: <Widget>[
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
                children: <Widget>[
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

// Classe de Dados para o Usuário (simplificada para este exemplo)
// Esta classe representa as informações do usuário.
class Usuario {
  String nome;
  String email;

  Usuario({required this.nome, required this.email});

  // Método para atualizar o usuário
  void update({String? newNome, String? newEmail}) {
    if (newNome != null) nome = newNome;
    if (newEmail != null) email = newEmail;
  }
}

// A Tela de Perfil de Usuário Simples e Autocontida
class PerfilUsuarioContentPage extends StatefulWidget {
  const PerfilUsuarioContentPage({Key? key}) : super(key: key);

  @override
  _PerfilUsuarioContentPageState createState() => _PerfilUsuarioContentPageState();
}

class _PerfilUsuarioContentPageState extends State<PerfilUsuarioContentPage> {
  // Estado interno do usuário para esta tela
  // Inicialização direta do objeto Usuario, resolvendo o LateInitializationError
  final Usuario _currentUser =
      Usuario(nome: 'Nome do Usuário', email: 'email@exemplo.com');

  final _formKey = GlobalKey<FormState>();
  late TextEditingController _nomeController;
  late TextEditingController _emailController;
  bool _isEditing = false; // Controla se a tela está em modo de edição

  @override
  void initState() {
    super.initState();
    // Inicializa os controladores de texto com os dados atuais do usuário
    _nomeController = TextEditingController(text: _currentUser.nome);
    _emailController = TextEditingController(text: _currentUser.email);
  }

  @override
  void dispose() {
    // É importante descartar os controladores para liberar recursos
    _nomeController.dispose();
    _emailController.dispose();
    super.dispose();
  }

  // Função para salvar as alterações do perfil
  void _salvarAlteracoes() {
    if (_formKey.currentState!.validate()) {
      setState(() {
        _currentUser.update(
          newNome: _nomeController.text,
          newEmail: _emailController.text,
        );
        _isEditing = false; // Sai do modo de edição após salvar
      });
      // Exibe uma mensagem de sucesso
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Perfil atualizado com sucesso!')),
      );
    }
  }

  // Função para cancelar o modo de edição e reverter para os dados originais
  void _cancelarEdicao() {
    setState(() {
      _isEditing = false;
      // Reseta os controladores para os valores que estavam antes da edição
      _nomeController.text = _currentUser.nome;
      _emailController.text = _currentUser.email;
    });
  }

  // Função de exemplo para Mudar Senha
  void _mudarSenha() {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Funcionalidade de mudar senha (ainda não implementada)')),
    );
    // Em um app real, você navegaria para uma tela de mudança de senha aqui.
  }

  // Função de exemplo para Configurações
  void _abrirConfiguracoes() {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Funcionalidade de configurações (ainda não implementada)')),
    );
    // Em um app real, você navegaria para uma tela de configurações aqui.
  }

  // Função para lidar com o logout
  void _handleLogout() {
    // Mostra um diálogo de confirmação antes de sair
    showDialog<void>(
      context: context,
      builder: (BuildContext context) => AlertDialog(
        title: const Text('Sair da Conta?'),
        content: const Text('Você tem certeza que deseja fazer logout?'),
        actions: <Widget>[
          TextButton(
            onPressed: () => Navigator.pop(context), // Fecha o diálogo
            child: const Text('Cancelar'),
          ),
          ElevatedButton(
            onPressed: () {
              Navigator.pop(context); // Fecha o diálogo
              // Aqui você implementaria a lógica de logout, como limpar tokens e navegar para a tela de login.
              ScaffoldMessenger.of(context).showSnackBar(
                const SnackBar(content: Text('Você fez logout.')),
              );
              // Exemplo de navegação para uma tela de login (simulada)
              // Navigator.pushReplacement(context, MaterialPageRoute(builder: (context) => LoginPage()));
            },
            style: ElevatedButton.styleFrom(backgroundColor: Colors.red),
            child: const Text('Sair', style: TextStyle(color: Colors.white)),
          ),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Meu Perfil'),
        backgroundColor: const Color(0xFF004675), // Azul escuro
        foregroundColor: Colors.white, // Cor do texto e ícones
        elevation: 0, // Remove a sombra da AppBar
        actions: <Widget>[
          // Botão Editar aparece quando NÃO estamos editando
          if (!_isEditing)
            IconButton(
              icon: const Icon(Icons.edit, color: Colors.white),
              onPressed: () {
                setState(() {
                  _isEditing = true; // Entra no modo de edição
                });
              },
            ),
          // Botões Cancelar e Salvar aparecem quando estamos editando
          if (_isEditing) ...<Widget>[
            IconButton(
              icon: const Icon(Icons.cancel, color: Colors.white),
              onPressed: _cancelarEdicao,
            ),
            IconButton(
              icon: const Icon(Icons.check, color: Colors.white),
              onPressed: _salvarAlteracoes,
            ),
          ],
        ],
      ),
      body: Container(
        // Gradiente de fundo que vai do azul escuro para o branco
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: const [const Color(0xFF004675), Colors.white], // Added const to the list
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(20.0), // Padding geral
          child: Form(
            key: _formKey, // Chave para o formulário para validação
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.center, // Centraliza os elementos
              children: <Widget>[
                const SizedBox(height: 20),
                // Avatar do Usuário
                const CircleAvatar(
                  radius: 60, // Tamanho do avatar
                  backgroundColor: Colors.white, // Fundo branco
                  child: Icon(
                    Icons.person,
                    size: 80,
                    color: Color(0xFF004675), // Ícone azul
                  ),
                ),
                const SizedBox(height: 20),
                // Nome do Usuário (sempre visível no cabeçalho)
                Text(
                  _currentUser.nome,
                  style: const TextStyle(
                    fontSize: 26,
                    fontWeight: FontWeight.bold,
                    color: Colors.white, // Texto branco para contraste
                  ),
                ),
                const SizedBox(height: 8),
                // Email do Usuário (sempre visível no cabeçalho)
                Text(
                  _currentUser.email,
                  style: const TextStyle(
                    fontSize: 18,
                    color: Colors.white70, // Texto branco mais suave
                  ),
                ),
                const SizedBox(height: 40),

                // Campo de entrada para o Nome
                _buildProfileInputField(
                  label: 'Nome Completo',
                  icon: Icons.person,
                  controller: _nomeController,
                  isEditable: _isEditing,
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return 'Por favor, insira seu nome';
                    }
                    return null;
                  },
                ),
                const SizedBox(height: 20),
                // Campo de entrada para o Email
                _buildProfileInputField(
                  label: 'Endereço de Email',
                  icon: Icons.email,
                  controller: _emailController,
                  isEditable: _isEditing,
                  validator: (String? value) {
                    if (value == null || value.isEmpty) {
                      return 'Por favor, insira seu email';
                    }
                    if (!value.contains('@')) {
                      return 'Email inválido';
                    }
                    return null;
                  },
                ),
                const SizedBox(height: 30),

                // Opções adicionais do perfil (Mudar Senha e Configurações)
                _buildListTileOption(
                  icon: Icons.lock,
                  title: 'Mudar Senha',
                  onTap: _mudarSenha,
                ),
                const SizedBox(height: 10), // Espaçamento entre as opções
                _buildListTileOption(
                  icon: Icons.settings,
                  title: 'Configurações',
                  onTap: _abrirConfiguracoes,
                ),
                const SizedBox(height: 40),

                // Botão de Sair da Conta
                TextButton.icon(
                  onPressed: _handleLogout,
                  icon: const Icon(Icons.logout, color: Colors.red, size: 24),
                  label: const Text(
                    'Sair da Conta',
                    style: TextStyle(color: Colors.red, fontSize: 18, fontWeight: FontWeight.bold),
                  ),
                  style: TextButton.styleFrom(
                    padding: const EdgeInsets.symmetric(horizontal: 25, vertical: 12),
                    shape: RoundedRectangleBorder(
                      borderRadius: BorderRadius.circular(12),
                      side: const BorderSide(color: Colors.red, width: 1.5), // Borda vermelha
                    ),
                  ),
                ),
                const SizedBox(height: 20),
              ],
            ),
          ),
        ),
      ),
    );
  }

  // Widget auxiliar para construir os campos de entrada do perfil (Nome/Email)
  Widget _buildProfileInputField({
    required String label,
    required IconData icon, // Parameter icon is used now
    required TextEditingController controller,
    required bool isEditable,
    String? Function(String?)? validator,
  }) {
    return TextFormField(
      controller: controller,
      readOnly: !isEditable, // Torna o campo somente leitura se não estiver editando
      decoration: InputDecoration(
        labelText: label,
        labelStyle: TextStyle(
            color: isEditable ? const Color(0xFF004675) : Colors.grey[700]),
        filled: true,
        fillColor: Colors.white.withAlpha((255 * 0.95).round()), // Fundo quase opaco
        border: const OutlineInputBorder( // Added const here
          borderRadius: const BorderRadius.all(Radius.circular(15.0)), // Fixed: Made BorderRadius const
          borderSide: BorderSide.none,
        ),
        prefixIcon: Icon(icon, color: const Color(0xFF004675)), // Used 'icon' parameter and added const to Color
        enabledBorder: OutlineInputBorder(
          borderRadius: BorderRadius.circular(15),
          borderSide: BorderSide(
            color: const Color(0xFF004675).withAlpha((255 * 0.6).round()),
            width: 1.5,
          ),
        ),
        focusedBorder: const OutlineInputBorder( // Added const here
          borderRadius: const BorderRadius.all(Radius.circular(15.0)), // Fixed: Made BorderRadius const
          borderSide: const BorderSide( // Added const here
            color: const Color(0xFF004675), // Added const here
            width: 2.5,
          ),
        ),
      ),
      style: TextStyle(
        color: isEditable ? Colors.black87 : Colors.grey[800],
        fontSize: 17,
        fontWeight: isEditable ? FontWeight.normal : FontWeight.w600, // Mais negrito quando não editável
      ),
      validator: validator,
    );
  }

  // Widget auxiliar para construir as opções de lista (Mudar Senha, Configurações)
  Widget _buildListTileOption({
    required IconData icon,
    required String title,
    required VoidCallback onTap,
  }) {
    return Container(
      decoration: BoxDecoration(
        color: Colors.white.withAlpha((255 * 0.95).round()), // Fundo quase opaco
        borderRadius: BorderRadius.circular(15), // Cantos arredondados
        boxShadow: <BoxShadow>[
          BoxShadow(
            color: Colors.black.withAlpha((255 * 0.05).round()),
            spreadRadius: 1,
            blurRadius: 5,
            offset: const Offset(0, 3), // Sombra suave
          ),
        ],
      ),
      child: ListTile(
        leading: Icon(icon, color: const Color(0xFF004675), size: 28),
        title: Text(
          title,
          style: const TextStyle(
            color: Color(0xFF004675),
            fontSize: 18,
            fontWeight: FontWeight.w600,
          ),
        ),
        trailing: const Icon(Icons.arrow_forward_ios, color: Colors.grey, size: 20),
        onTap: onTap,
        contentPadding: const EdgeInsets.symmetric(horizontal: 20, vertical: 8),
      ),
    );
  }
}
