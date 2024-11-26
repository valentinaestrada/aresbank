import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle, CardDescription } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs';
import { Bell, CreditCard, Globe, Mail, Phone, User, Users, UserCheck } from 'lucide-react';

const AresBankPlatform = () => {
  const [currentView, setCurrentView] = useState('userType');
  const [userType, setUserType] = useState(null);
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [language, setLanguage] = useState('es');

  const renderUserTypeSelection = () => (
    <div className="container mx-auto p-4 max-w-4xl">
      <div className="text-center mb-8">
        <h1 className="text-3xl font-bold mb-2">
          {language === 'es' ? 'Bienvenido a Aresbank' : 'Welcome to Aresbank'}
        </h1>
        <p className="text-gray-600">
          {language === 'es' 
            ? 'Por favor, seleccione su tipo de usuario para continuar' 
            : 'Please select your user type to continue'}
        </p>
      </div>
      
      <div className="grid md:grid-cols-2 gap-6">
        <Card className="hover:shadow-lg transition-shadow">
          <CardHeader>
            <CardTitle className="flex items-center">
              <User className="mr-2" />
              {language === 'es' ? 'Cliente' : 'Client'}
            </CardTitle>
            <CardDescription>
              {language === 'es' 
                ? 'Acceso para empresas y particulares que mantienen una relación bancaria directa con Aresbank. Incluye servicios como:'
                : 'Access for companies and individuals who maintain a direct banking relationship with Aresbank. Includes services such as:'}
            </CardDescription>
          </CardHeader>
          <CardContent>
            <ul className="list-disc pl-5 space-y-2 mb-4">
              <li>{language === 'es' ? 'Gestión de cuentas bancarias' : 'Bank account management'}</li>
              <li>{language === 'es' ? 'Créditos documentarios' : 'Documentary credits'}</li>
              <li>{language === 'es' ? 'Transferencias internacionales' : 'International transfers'}</li>
            </ul>
            <Button 
              className="w-full" 
              onClick={() => {
                setUserType('client');
                setCurrentView('login');
              }}
            >
              {language === 'es' ? 'Continuar como Cliente' : 'Continue as Client'}
            </Button>
          </CardContent>
        </Card>

        <Card className="hover:shadow-lg transition-shadow">
          <CardHeader>
            <CardTitle className="flex items-center">
              <UserCheck className="mr-2" />
              {language === 'es' ? 'Beneficiario' : 'Beneficiary'}
            </CardTitle>
            <CardDescription>
              {language === 'es'
                ? 'Acceso para beneficiarios de créditos documentarios y otros servicios. Permite:'
                : 'Access for beneficiaries of documentary credits and other services. Allows:'}
            </CardDescription>
          </CardHeader>
          <CardContent>
            <ul className="list-disc pl-5 space-y-2 mb-4">
              <li>{language === 'es' ? 'Consulta de créditos documentarios' : 'Documentary credit consultation'}</li>
              <li>{language === 'es' ? 'Gestión de documentación' : 'Documentation management'}</li>
              <li>{language === 'es' ? 'Seguimiento de operaciones' : 'Operation tracking'}</li>
            </ul>
            <Button 
              className="w-full" 
              onClick={() => {
                setUserType('beneficiary');
                setCurrentView('login');
              }}
            >
              {language === 'es' ? 'Continuar como Beneficiario' : 'Continue as Beneficiary'}
            </Button>
          </CardContent>
        </Card>
      </div>

      <div className="mt-6 flex justify-center">
        <Button 
          variant="outline" 
          onClick={() => setLanguage(language === 'es' ? 'en' : 'es')}
          className="flex items-center"
        >
          <Globe className="w-4 h-4 mr-2" />
          {language === 'es' ? 'Switch to English' : 'Cambiar a Español'}
        </Button>
      </div>
    </div>
  );

  const renderLoginForm = () => (
    <Card className="w-full max-w-md mx-auto">
      <CardHeader>
        <CardTitle className="text-2xl font-bold text-center">
          {language === 'es' 
            ? `Iniciar Sesión como ${userType === 'client' ? 'Cliente' : 'Beneficiario'}`
            : `Login as ${userType === 'client' ? 'Client' : 'Beneficiary'}`}
        </CardTitle>
      </CardHeader>
      <CardContent>
        <div className="space-y-4">
          <Input 
            type="text" 
            placeholder={language === 'es' ? 'Usuario' : 'Username'} 
            className="w-full"
          />
          <Input 
            type="password" 
            placeholder={language === 'es' ? 'Contraseña' : 'Password'} 
            className="w-full"
          />
          <Button 
            className="w-full" 
            onClick={() => setIsLoggedIn(true)}
          >
            {language === 'es' ? 'Entrar' : 'Sign In'}
          </Button>
          {userType === 'client' && (
            <Button 
              variant="outline" 
              className="w-full"
              onClick={() => setCurrentView('register')}
            >
              {language === 'es' ? 'Registrarse' : 'Register'}
            </Button>
          )}
          <Button 
            variant="ghost" 
            className="w-full"
            onClick={() => setCurrentView('userType')}
          >
            {language === 'es' ? 'Volver' : 'Back'}
          </Button>
        </div>
      </CardContent>
    </Card>
  );

  // El resto del código permanece igual...
  // (renderRegistrationForm, renderDashboard, etc.)

  switch (currentView) {
    case 'userType':
      return renderUserTypeSelection();
    case 'login':
      return renderLoginForm();
    case 'register':
      return renderRegistrationForm();
    default:
      return renderDashboard();
  }
};

export default AresBankPlatform;
