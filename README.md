# Chat-IA
Chat bot
// Instantiate a Google sign-in request
val googleIdOption = GetGoogleIdOption.Builder()
    // Your server's client ID, not your Android client ID.
    .setServerClientId(getString(R.string.default_web_client_id))
    // Only show accounts previously used to sign in.
    .setFilterByAuthorizedAccounts(true)
    .build()

// Create the Credential Manager request
val request = GetCredentialRequest.Builder()
    .addCredentialOption(googleIdOption)
    .build() import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_auth/firebase_auth.dart';
import 'package:cloud_firestore/cloud_firestore.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'App de Chat',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: StreamBuilder<User?>(
        stream: FirebaseAuth.instance.authStateChanges(),
        builder: (context, snapshot) {
          if (snapshot.hasData) {
            return ChatScreen();
          } else {
            return LoginScreen();
          }
        },
      ),
    );
  }
}
