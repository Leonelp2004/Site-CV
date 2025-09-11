<template>
  <div id="app">
    <!-- NAVBAR -->
    <nav>
      <div class="logo">Leonel José Coelho Pinheiro</div>
      <ul>
        <li><a href="#sobre-mim">Sobre</a></li>
        <li><a href="#experiencia">Experiência</a></li>
        <li><a href="#formacao">Formação</a></li>
        <li><a href="#projetos">Projetos</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#extras">Idiomas/Certificações</a></li>
        <li><strong><li><a href='/CV_Leonel-Pinheiro.pdf' class="download-btn" download>Download CV</a>
</li>
</strong></li>
      </ul>
      <div class="search-container">
        <span class="search-icon" @click="toggleSearch"></span>
        <input
          v-model="searchQuery"
          :class="{ active: searchActive }"
          type="text"
          placeholder="Pesquisar projetos/skills..."
        />
      </div>
    </nav>

    <div class="container">
      <!-- SOBRE MIM -->
      <Accordion title="Sobre Mim" :defaultOpen="true">
        <section id="sobre-mim" class="about">
        <div class="about">
          <div class="about-content">
            <h2>BSc in Information Systems Engineering and Management | University of Minho</h2>
            <p>
              Chamo-me <strong>Leonel Pinheiro</strong>, tenho <strong>21 anos</strong> e resido em <strong>Amares, Braga</strong>.
              Sou recém licenciado em <strong><a href='https://legsi.dsi.uminho.pt/'target= 'blank'>Engenharia e Gestão de Sistemas de Informação</a></strong>. Tenho procurado,
              ao longo do meu percurso académico e profissional, desenvolver continuamente as minhas
              competências técnicas e interpessoais, com o objetivo de me tornar uma mais-valia em
              projetos futuros, seja na área de desenvolvimento de software ou em qualquer outro contexto.
              Ao longo da minha jornada já participei em várias ações de voluntariado, nomeadamente no
              projeto Missão Amar(es), bem como num concurso de empreendedorismo <strong><a href= 'https://www.cimcavado.pt/up-cavado/' target= 'blank'>UP Cávado</a></strong> alcançando
              a terceira colocação.
            </p>
          </div>
          <div class="about-image">
           <img src="/Foto tipo passe.jpg" alt="Foto de Perfil" class="profile-pic"/>

          </div>
        </div>
        </section>
      </Accordion>

      <!-- EXPERIÊNCIA -->
      <Accordion title="Experiência Profissional">
        <section id="experiencia" class="accordion-section">
        <div class="accordion-section">
          <div v-for="(exp, i) in experiences" :key="i" class="card">
            <div class="card-header">
              <h3>{{ exp.empresa }}</h3>
              <span>{{ exp.periodo }}</span>
            </div>
            <p class="card-role">{{ exp.cargo }}</p>
            <p>{{ exp.descricao }}</p>
          </div>
        </div>
        </section>
      </Accordion>

      <!-- FORMAÇÃO -->
      <Accordion title="Formação">
        <section id="formacao" class="accordion-section">
        <div class="accordion-section">
          <div v-for="(form, i) in education" :key="i" class="card">
            <div class="card-header">
              <h3>{{ form.instituicao }}</h3>
              <span>{{ form.periodo }}</span>
            </div>
            <p class="card-role">{{ form.curso }}</p>
          </div>
        </div>
        </section>
      </Accordion>

      <!-- SKILLS -->
      
    <Accordion title="Skills / Competências">
      <section id="skills" class="accordion-section"></section>
      <div class="skills-container">
        <div class="skills-column" v-for="(col, index) in 2" :key="index">
          <div v-for="(skill, i) in skills.filter((_, idx) => idx % 2 === index)" :key="i" class="skill-bar">
            <span class="skill-name">{{ skill.nome }}</span>
            <div class="skill-level">
              <div class="skill-progress" :style="{ width: skill.nivel + '%' }"></div>
            </div>
          </div>
        </div>
      </div>
    </Accordion>



      <!-- PROJETOS -->
      <Accordion title="Projetos / Portfólio">
        <section id="projetos">
        <div class="accordion-section">
          <div v-for="(proj, i) in filteredProjects" :key="i" class="card">
            <h3>{{ proj.nome }}</h3>
            <a :href="proj.link" target="_blank" class="download-btn">Clique aqui para consultar alguns dos projetos que desenvolvi</a> 
            <p>{{ proj.descricao }}</p>
          </div>
        </div>
        </section>
      </Accordion>
      

    <Accordion title="Idiomas/Certificações">
      <section id="extras">
  <div class="accordion-section">
    <div class="card"><strong>Idiomas:</strong> {{ extras.idiomas }}</div>
    
    <div class="card">
      <strong>Certificações:</strong>
      <ul class="cert-list">
        <li v-for="(cert, i) in extras.certificacoes" :key="i">
          <span>{{ cert.nome }}</span>
          <br></br>
          <a :href="cert.link" target="_blank" class="download-btn" download>Ver Certificado</a>
          <br></br>
        </li>
      </ul>
    </div>
  </div>
  </section>
</Accordion>
    </div>
<!-- CHAT WIDGET -->
   <!-- Chat Widget -->
<div class="chat-widget" :class="{ open: chatOpen }">
  <div class="chat-header" @click="toggleChat">
    Chat Bot "Sobre Mim"
  </div>

  <!-- Corpo do chat -->
  <div class="chat-body" ref="messagesContainer">
    <div v-for="(msg, i) in messages" :key="i" :class="['message', msg.type]">
      {{ msg.text }}
    </div>
  </div>

  <!-- Campo de envio -->
  <div class="chat-input">
    <textarea
      v-model="userMessage"
      placeholder="Indique o que deseja saber sobre mim..."
      rows="2"
    ></textarea>
    <button @click="sendMessage"><strong>Enviar</strong></button>
  </div>
</div>




    <!-- FOOTER -->
<footer class="site-footer">
  <div class="footer-contact">
    <div class="contact-item">
      <span class="icon">📧</span>
      <a href="https://mail.google.com/mail/u/0/#sent?compose=CllgCKHQdVwxJzZwWjQNzwrKbpBmTMRGFzxnhQXNTRCQDMclMqtqlhBpZcdXzVGlcHqnbTjngKL">leonelp2004@gmail.com</a>
    </div>
    <div class="contact-item">
      <span class="icon">📱</span>
      <a href="tel:+351924476311">+351 924 476 311</a>
    </div>
    <div class="contact-item">
      <span class="icon">🔗</span>
      <a href="https://www.linkedin.com/in/leonel-pinheiro" target="_blank">LinkedIn</a>
    </div>
    <div class="contact-item">
      <span class="icon">🐱</span>
      <a href="https://github.com/Leonelp2004/Projetos.git" target="_blank">GitHub</a>
    </div>
  </div>
</footer>
  </div>
</template>

<script setup>
import { ref, computed, nextTick } from 'vue'
import Accordion from './components/Accordion.vue'
import SkillTag from './components/SkillTag.vue'

// EXPERIÊNCIAS
const experiences = [
  {
    empresa:'Empresa Grupo Casais',
    cargo:'Summer Internship',
    periodo:'Jun 2025 - Set 2025',
    descricao:'Durante o estágio de verão, desenvolvi um projeto de automação para a criação e distribuição de vídeos técnicos em português e inglês, utilizando o HeyGen e a Gemini API, integrados com ferramentas como ServiceDesk+, Power Automate, SharePoint, Teams e Outlook. Paralelamente, desenvolvi um agente inteligente de suporte IT (CSI) no Copilot Studio, integrado com ServiceDesk+, Power Automate, SharePoint, OneDrive, Teams e HeyGen, permitindo a gestão de tickets, envio de notificações e disponibilização de soluções multimédia de forma eficiente.'
  }
]

// FORMAÇÃO
const education = [
  { instituicao:'Escola Secundária de Amares', curso:'Curso de Ciências e Tecnologias', periodo:'Set 2019 - Jun 2022' },
  { instituicao:'Universidade do Minho', curso:'Licenciatura em Engenharia e Gestão de Sistemas de Informação', periodo:'Set 2022 - Jun 2025' }
]

// SKILLS
const skills = [
  { nome: 'HTML, CSS, JS, Vue.js', nivel: 85 },
  { nome: 'Python', nivel: 75 },
  { nome: 'SQL', nivel: 75 },
  { nome: 'SAP', nivel: 65 },
  { nome: 'Java', nivel: 70 },
  { nome: 'Tableau', nivel: 80 },
  { nome: 'C++', nivel: 65 },
  { nome: 'Prolog', nivel: 55 },
  { nome: 'Power Apps', nivel: 80 }
]

// PROJETOS
const projects = [
  {
    nome:'Projetos Universitários',
    link:'https://github.com/Leonelp2004/Projetos.git',
    descricao: '- Algoritmos e Estruturas de Dados (Projeto em C++)\n- Sistemas de Computação (Projeto em Assembly)\n- Bases de Dados (Projeto em SQL e Cassandra)\n- Processo e Metodologias de Software (Projeto com ferramentas de modelação (UML))\n- Programação com Objetos (Projeto em Java)\n- Sistemas Operativos (Projeto em Linux)\n- Introdução às Redes de Computadores (Projeto envolvendo protocolos: TCP/IP, HTTP, DHCP)\n- Desenvolvimento de Aplicações Informáticas (Projeto em HTML, CSS, JS)\n- Implantação de Aplicações Informáticas Empresariais (Projeto em SAP, React, Moloni, JSON)\n- Engenharia de Dados para Suporte a Tomada de Decisão (Projeto em SQL, Jupyter, Tableau, Hadoop, Spark)\n- Fundamentos de Sistemas de Informação (Projeto em Python)\n- Programação Web (Projeto em HTML, CSS, JS, Vue.js)\n- Desenvolvimento Organizacional de Tecnologias de Informação (Projeto com modelação de processos, ERPs, CRMs)\n- Técnicas de Inteligência Artificial (Projeto em Prolog)',
    tags:'universitario html css js'
  },
  {
    nome:'Projetos Estágio Profissional',
    link:'https://github.com/Leonelp2004/Projetos.git',
    descricao:'Projeto de automação da criação e distribuição de vídeos técnicos (PT/EN), através da integração da HeyGen API e Gemini API com ServiceDesk+, Power Automate, SharePoint, Teams, Outlook e OneDrive. As principais funcionalidades implementadas incluíram: • Obtenção automática dos boletins técnicos no ServiceDesk+; • Verificação da existência de vídeos associados a um dado boletim; • Geração automática do guião do orador e mensagens de apoio; • Produção de vídeos AI em PT/EN; • Armazenamento no OneDrive/SharePoint; • Criação de links de partilha e comunicação automática via Teams e Outlook com thumbnails; • Atualização do boletim técnico no CSI com os links dos vídeos. Posteriormente, desenvolvi o CSI BOT – Agente de Suporte IT Inteligente, um chat Bot criado no Copilot Studio com fluxos em Power Automate, integrando-se com ServiceDesk+, OneDrive, SharePoint, Outlook e Teams. O agente foi concebido para: • Obter informações de atualizações recentes de tickets • Consultar estado/detalhes de tickets/pedidos • Criar novos tickets por via conversacional • Detalhes/resumos/atualizações de boletins técnicos • Disponibilizar vídeos Heygen de um boletim técnico • Criar vídeos HeyGen (apenas para colaboradores autorizados) • Informações gerais da DSI • Informações colaboradores DSI/HELPDESK • Consultar id de um dado boletim • Consultar id de um dado ticket • Resolução de problemas relacionados com tickets • Histórico de conversas de um dado ticket • Enviar mensagens Teams com o conteúdo que o utilizador desejar • Enviar email Outlook ao utilizador ou criar rascunho',
    tags:'profissional vue js'
  }
]

// EXTRAS
const extras = {
  idiomas: 'Português (Nativo), Inglês (Intermédio B2)',
  certificacoes: [
    { nome: 'Certificate of Language Proficiency (English)', link: '/certificado.pdf' },
    { nome: 'Certificado de termino de curso', link: '/Certidão.pdf' }
  ],
  bot: 'Disponível no site para perguntas rápidas sobre meu CV.'
}

// PESQUISA
const searchQuery = ref('')
const searchActive = ref(false)
const toggleSearch = () => (searchActive.value = !searchActive.value)

const filteredProjects = computed(() => {
  if (!searchQuery.value) return projects
  return projects.filter(p => (p.nome + ' ' + p.tags + ' ' + p.descricao)
    .toLowerCase().includes(searchQuery.value.toLowerCase()))
})

// CHAT BOT
const chatOpen = ref(false)
const userMessage = ref('')
const messages = ref([])
const messagesContainer = ref(null)

const toggleChat = () => {
  chatOpen.value = !chatOpen.value
  nextTick(scrollToBottom)
}

const scrollToBottom = () => {
  if (messagesContainer.value) messagesContainer.value.scrollTop = messagesContainer.value.scrollHeight
}

const sendMessage = async () => {
  if (!userMessage.value.trim()) return
  messages.value.push({ type: 'user', text: userMessage.value })
  const msg = userMessage.value
  userMessage.value = ''
  nextTick(scrollToBottom)

  try {
    const response = await fetch(
      'https://leonelp2004.app.n8n.cloud/webhook/8a1aac86-a4ee-4583-a674-2722dfba077b/chat',
      { method: 'POST', headers:{'Content-Type':'application/json'}, body:JSON.stringify({ message: msg }) }
    )
    const data = await response.json()
    messages.value.push({ type: 'bot', text: data.reply || 'Sem resposta.' })
    nextTick(scrollToBottom)
  } catch (err) {
    messages.value.push({ type: 'bot', text: 'Erro ao conectar com o bot.' })
    nextTick(scrollToBottom)
    console.error(err)
  }
}

</script>



<style scoped>
/* MENU MOBILE */
.menu-toggle {
  display: none;
  font-size: 1.8rem;
  background: none;
  border: none;
  color: #fff;
  cursor: pointer;
}

nav ul {
  display: flex;
  gap: 40px;
}

@media (max-width: 1423px) {
  .menu-toggle {
    display: block;
    font-size: 1.5rem; 
  }

  nav ul {
    display: none;
    flex-direction: column;
    width: 100%;
    margin-top: 8px;
    gap: 8px; 
  }

  nav ul.show {
    display: flex;
  }

  nav ul li a,
  .download-btn {
    width: 100%;
    text-align: center;
    padding: 8px 8px; 
    font-size: 0.7rem; 
  }
  .chat-widget {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 180px;
  height: 50px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 5px 20px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  transition: height 0.3s ease;
  font-family: Arial, sans-serif;
  z-index: 1000;
}
.chat-widget.open { height: 400px; }
}

</style>

