import 'package:flutter/material.dart';

void main() {
  runApp(const AsuraAIApp());
}

class AsuraAIApp extends StatelessWidget {
  const AsuraAIApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        brightness: Brightness.dark,
        scaffoldBackgroundColor: const Color(0xFF212121),
      ),
      home: const ChatScreen(),
    );
  }
}

class ChatScreen extends StatefulWidget {
  const ChatScreen({super.key});

  @override
  State<ChatScreen> createState() => _ChatScreenState();
}

class _ChatScreenState extends State<ChatScreen> {
  final TextEditingController _controller = TextEditingController();
  
  // Chat History (ဘယ်ဘက် Sidebar မှာ ပြသမည့် ရှေ့ဟောင်း Chat များ)
  final List<String> _chatSessions = [
    "Asura AI App တည်ဆောက်ခြင်း",
    "Flutter UI ဒီဇိုင်းဆွဲနည်း",
    "ChatGPT API ချိတ်ဆက်ခြင်း",
  ];
  
  final List<Map<String, dynamic>> _messages = [
    {"role": "assistant", "content": "မင်္ဂလာပါ မောင်ရေ။ Asura AI ကနေ ဘာများ ကူညီပေးရမလဲ?"},
  ];

  void _sendMessage() {
    if (_controller.text.trim().isEmpty) return;
    setState(() {
      _messages.add({"role": "user", "content": _controller.text, "type": "text"});
      _controller.clear();
    });

    // Simulate AI response
    Future.delayed(const Duration(seconds: 1), () {
      setState(() {
        _messages.add({
          "role": "assistant", 
          "content": "မောင်ပြောတာကို လက်ခံရရှိပါပြီဗျ။ ဆက်လက် လုပ်ဆောင်ပေးနေပါပြီ။", 
          "type": "text"
        });
      });
    });
  }

  // ပုံ သို့မဟုတ် ဖိုင်တင်ရန် နှိပ်သည့်အခါ
  void _showAttachmentOptions() {
    showModalBottomSheet(
      context: context,
      backgroundColor: const Color(0xFF2f2f2f),
      shape: const RoundedRectangleBorder(
        borderRadius: BorderRadius.vertical(top: Radius.circular(20)),
      ),
      builder: (context) {
        return Container(
          padding: const EdgeInsets.all(20),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              const Text(
                'ဖိုင် သို့မဟုတ် ပုံ ထည့်သွင်းရန်',
                style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold, color: Colors.white),
              ),
              const SizedBox(height: 20),
              ListTile(
                leading: const Icon(Icons.image, color: Colors.blueAccent),
                title: const Text('ဓာတ်ပုံ (Gallery / Camera)', style: TextStyle(color: Colors.white)),
                onTap: () {
                  Navigator.pop(context);
                  // TODO: image_picker ကုဒ် ဆက်ထည့်ရန်
                  ScaffoldMessenger.of(context).showSnackBar(
                    const SnackBar(content: Text('ဓာတ်ပုံရွေးချယ်မှုကို ချိတ်ဆက်နေပါပြီ...')),
                  );
                },
              ),
              ListTile(
                leading: const Icon(Icons.insert_drive_file, color: Colors.orangeAccent),
                title: const Text('စာရွက်စာတမ်း ဖိုင် (PDF/Doc)', style: TextStyle(color: Colors.white)),
                onTap: () {
                  Navigator.pop(context);
                  // TODO: file_picker ကုဒ် ဆက်ထည့်ရန်
                  ScaffoldMessenger.of(context).showSnackBar(
                    const SnackBar(content: Text('ဖိုင်ရွေးချယ်မှုကို ချိတ်ဆက်နေပါပြီ...')),
                  );
                },
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
        backgroundColor: const Color(0xFF212121),
        elevation: 0,
        title: const Row(
          mainAxisSize: MainAxisSize.min,
          children: [
            Text('Asura AI', style: TextStyle(fontSize: 18, fontWeight: FontWeight.w600)),
            SizedBox(width: 4),
            Icon(Icons.sparkles, size: 16, color: Colors.amber),
          ],
        ),
        centerTitle: true,
        actions: [
          IconButton(
            icon: const Icon(Icons.add, color: Colors.white),
            onPressed: () {
              setState(() {
                _messages.clear();
                _messages.add({"role": "assistant", "content": "Chat အသစ် စတင်လိုက်ပါပြီ မောင်။"});
              });
            },
            tooltip: "New Chat",
          ),
        ],
      ),
      
      // ဘယ်ဘက် Sidebar (Chat History Drawer)
      drawer: Drawer(
        backgroundColor: const Color(0xFF171717),
        child: ListView(
          padding: EdgeInsets.zero,
          children: [
            const DrawerHeader(
              decoration: BoxDecoration(color: Color(0xFF212121)),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                mainAxisAlignment: MainAxisAlignment.end,
                children: [
                  Text(
                    'Asura AI',
                    style: TextStyle(color: Colors.white, fontSize: 22, fontWeight: FontWeight.bold),
                  ),
                  SizedBox(height: 4),
                  Text(
                    'Chat History များနှင့် မှတ်တမ်းများ',
                    style: TextStyle(color: Colors.grey, fontSize: 13),
                  ),
                ],
              ),
            ),
            ListTile(
              leading: const Icon(Icons.add, color: Colors.white),
              title: const Text('New chat', style: TextStyle(color: Colors.white)),
              onTap: () {
                Navigator.pop(context);
                setState(() {
                  _messages.clear();
                  _messages.add({"role": "assistant", "content": "Chat အသစ် စတင်လိုက်ပါပြီ မောင်။"});
                });
              },
            ),
            const Divider(color: Colors.grey),
            const Padding(
              padding: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
              child: Text('Recent', style: TextStyle(color: Colors.grey, fontSize: 12, fontWeight: FontWeight.bold)),
            ),
            ..._chatSessions.map((title) => ListTile(
              leading: const Icon(Icons.message_outlined, color: Colors.grey, size: 20),
              title: Text(title, style: const TextStyle(color: Colors.white70, fontSize: 14)),
              onTap: () {
                Navigator.pop(context);
                // နှိပ်လိုက်သော Chat History သို့ ပြောင်းရန် နေရာ
              },
            )),
          ],
        ),
      ),

      body: Column(
        children: [
          // Chat Messages List Area
          Expanded(
            child: ListView.builder(
              padding: const EdgeInsets.all(16),
              itemCount: _messages.length,
              itemBuilder: (context, index) {
                final msg = _messages[index];
                final isUser = msg['role'] == 'user';
                return Container(
                  margin: const EdgeInsets.symmetric(vertical: 6),
                  alignment: isUser ? Alignment.centerRight : Alignment.centerLeft,
                  child: Container(
                    padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                    constraints: BoxConstraints(maxWidth: MediaQuery.of(context).size.width * 0.75),
                    decoration: BoxDecoration(
                      color: isUser ? const Color(0xFF2f2f2f) : Colors.transparent,
                      borderRadius: BorderRadius.circular(16),
                    ),
                    child: Text(
                      msg['content']!,
                      style: const TextStyle(fontSize: 15, color: Colors.white),
                    ),
                  ),
                );
              },
            ),
          ),

          // ChatGPT Style Input Bar + Attachment Button
          Container(
            padding: const EdgeInsets.all(12),
            color: const Color(0xFF212121),
            child: SafeArea(
              child: Row(
                children: [
                  // Attachment Button (Plus Icon)
                  IconButton(
                    icon: const Icon(Icons.add_circle_outline, color: Colors.grey, size: 24),
                    onPressed: _showAttachmentOptions,
                    tooltip: "Add Photo or File",
                  ),
                  
                  // Text Field Input
                  Expanded(
                    child: Container(
                      padding: const EdgeInsets.symmetric(horizontal: 16),
                      decoration: BoxDecoration(
                        color: const Color(0xFF2f2f2f),
                        borderRadius: BorderRadius.circular(24),
                      ),
                      child: TextField(
                        controller: _controller,
                        style: const TextStyle(color: Colors.white),
                        decoration: const InputDecoration(
                          hintText: 'Message Asura AI...',
                          hintStyle: TextStyle(color: Colors.grey),
                          border: InputBorder.none,
                        ),
                      ),
                    ),
                  ),
                  const SizedBox(width: 8),
                  
                  // Send Button
                  GestureDetector(
                    onTap: _sendMessage,
                    child: Container(
                      padding: const EdgeInsets.all(10),
                      decoration: const BoxDecoration(
                        color: Colors.white,
                        shape: BoxShape.circle,
                      ),
                      child: const Icon(Icons.arrow_upward, color: Colors.black, size: 20),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }
}
