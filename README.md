
# 📄 PDF Generator

Projeto em **React + Vite** para geração e download de arquivos PDF a partir de componentes da aplicação.

---

## 🚀 Tecnologias Utilizadas

* [React](https://reactjs.org/)
* [Vite](https://vitejs.dev/)
* [html2canvas](https://github.com/niklasvh/html2canvas)
* [jsPDF](https://github.com/parallax/jsPDF)

---

## ⚙️ Requisitos

* Node.js **>= 20.9.0** ou **>= 18.18.0**
* npm **>= 9**

---

Instale as dependências:

```bash
npm install
```

---

## ▶️ Rodando o projeto em desenvolvimento

```bash
npm run dev
```

Abra no navegador:
👉 [http://localhost:5173](http://localhost:5173)

---

## 🖨️ Como funciona a geração de PDF

1. O componente é renderizado na tela.
2. A biblioteca **html2canvas** captura o conteúdo como imagem.
3. O **jsPDF** gera um arquivo PDF a partir dessa imagem.
4. O usuário pode fazer download clicando em um botão.

Exemplo de uso:

```tsx
import html2canvas from "html2canvas";
import jsPDF from "jspdf";
import React from "react";

export default function Invoice() {
  const printRef = React.useRef(null);

  const handleDownloadPdf = async () => {
    const element = printRef.current;
    if (!element) return;

    const canvas = await html2canvas(element);
    const data = canvas.toDataURL("image/png");

    const pdf = new jsPDF("p", "mm", "a4");
    pdf.addImage(data, "PNG", 0, 0, 210, 297); // A4 size
    pdf.save("documento.pdf");
  };

  return (
    <div>
      <div ref={printRef}>
        <h1>Meu Documento</h1>
        <p>Conteúdo que será exportado em PDF.</p>
      </div>
      <button onClick={handleDownloadPdf}>Baixar PDF</button>
    </div>
  );
}
```

---

## 📂 Estrutura do Projeto

```
pdf-generator/
│── src/
│   ├── components/   # Componentes reutilizáveis
│   ├── App.tsx       # Componente principal
│   └── main.tsx      # Ponto de entrada
│── index.html
│── package.json
│── vite.config.ts
│── README.md
```

