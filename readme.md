/**
 * 🖨️ PRINT CSS PRO HRD REPORT - OPRAVENÁ VERZE
 * 
 * POUŽITÍ:
 * 1. Otevři DevTools (F12)
 * 2. Přejdi na záložku Console
 * 3. Zkopíruj celý tento kód
 * 4. Vlož do konzole a stiskni Enter
 * 5. Stiskni Ctrl+P a ulož jako PDF
 */

(function() {
  'use strict';
  
  console.log('📄 Načítám print CSS pro HRD report...');
  
  if (document.getElementById('dynamic-print-css')) {
    console.warn('⚠️  Print CSS už je načtené!');
    console.log('💡 Můžeš rovnou tisknout: Ctrl+P');
    return;
  }
  
  const reportElement = document.querySelector('.es-report-container .ibox-content');
  if (!reportElement) {
    console.error('❌ Report nebyl nalezen!');
    return;
  }
  
  const printCSS = `
    @page {
      size: A4 portrait;
      margin: 10mm 8mm;
    }

    @media print {
      /* Skryj vše kromě reportu */
      body * {
        visibility: hidden;
      }
      
      .es-report-container,
      .es-report-container * {
        visibility: visible;
      }
      
      .es-report-container {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        margin: 0;
        padding: 0;
      }
      
      .es-report-container .ibox,
      .es-report-container .ibox-content {
        margin: 0;
        padding: 0;
        border: none;
        box-shadow: none;
      }
      
      /* Základní styly pro tisk */
      body {
        margin: 0;
        padding: 0;
        background: white;
        color: #000;
        font-size: 9.5pt;
        line-height: 1.25;
        font-family: Arial, sans-serif;
      }
      
      /* Černobílý tisk s výjimkami */
      * {
        box-shadow: none !important;
        text-shadow: none !important;
      }
      
      /* Červené nadpisy */
      .colored,
      h2,
      h3.colored {
        color: #c00 !important;
        background: white !important;
      }
      
      /* Ostatní text černý */
      p, div, span, label, td, th {
        color: #000 !important;
        background: white !important;
      }
      
      /* FORMULÁŘOVÁ POLE - klíčová oprava */
      .form-control,
      input[type="text"],
      input[type="email"],
      input[type="tel"],
      input[type="number"],
      input[type="date"],
      textarea,
      select {
        border: none !important;
        border-bottom: 1px solid #ddd !important;
        background: transparent !important;
        padding: 1pt 0 !important;
        margin: 0 !important;
        font-size: 9.5pt !important;
        font-family: Arial, sans-serif !important;
        color: #000 !important;
        -webkit-appearance: none !important;
        -moz-appearance: none !important;
        appearance: none !important;
        box-shadow: none !important;
        height: auto !important;
        line-height: 1.25 !important;
      }
      
      /* Labely formulářů */
      .col-form-label,
      label {
        font-weight: 500 !important;
        font-size: 8.5pt !important;
        color: #000 !important;
        background: transparent !important;
        padding: 1pt 0 !important;
      }
      
      .es-report-important {
        font-weight: 700 !important;
        color: #000 !important;
      }
      
      /* BOOTSTRAP GRID - zachování layoutu */
      .row {
        display: flex !important;
        flex-wrap: wrap !important;
        margin: 0 -5pt !important;
      }
      
      .col-lg-12,
      .col-md-12 {
        width: 100% !important;
        padding: 0 5pt !important;
      }
      
      .col-lg-6,
      .col-md-6 {
        width: 50% !important;
        padding: 0 5pt !important;
        float: left !important;
      }
      
      .col-lg-4 {
        width: 33.333% !important;
        padding: 0 5pt !important;
        float: left !important;
      }
      
      .col-lg-8 {
        width: 66.666% !important;
        padding: 0 5pt !important;
        float: left !important;
      }
      
      .col-sm-3,
      .col-sm-4 {
        width: 35% !important;
        padding: 0 5pt !important;
        float: left !important;
      }
      
      .col-sm-6 {
        width: 50% !important;
        padding: 0 5pt !important;
        float: left !important;
      }
      
      .col-sm-8,
      .col-sm-9 {
        width: 65% !important;
        padding: 0 5pt !important;
        float: left !important;
      }
      
      /* Form groups */
      .form-group {
        display: flex !important;
        flex-wrap: nowrap !important;
        align-items: center !important;
        margin-bottom: 2pt !important;
        page-break-inside: avoid !important;
      }
      
      .form-group.row {
        display: flex !important;
      }
      
      /* TABULKY */
      table {
        width: 100% !important;
        border-collapse: collapse !important;
        page-break-inside: auto !important;
        margin: 4pt 0 !important;
        font-size: 8.5pt !important;
      }
      
      /* Opakování hlavičky na každé stránce */
      thead {
        display: table-header-group !important;
      }
      
      tbody {
        display: table-row-group !important;
      }
      
      tfoot {
        display: table-footer-group !important;
      }
      
      /* Řádky tabulky - nerozbíjej je */
      tr {
        page-break-inside: avoid !important;
        page-break-after: auto !important;
      }
      
      /* Celé tabulky - pokus se nevlomit, ale pokud musíš, tak pokračuj */
      .es-table-wrapper table {
        page-break-before: auto !important;
        page-break-after: auto !important;
        page-break-inside: auto !important;
      }
      
      th, td {
        padding: 3pt 5pt !important;
        border: 1px solid #333 !important;
        text-align: left !important;
        vertical-align: top !important;
        color: #000 !important;
      }
      
      th {
        font-weight: bold !important;
        background: #f0f0f0 !important;
        color: #000 !important;
      }
      
      td {
        background: white !important;
      }
      
      .align-right {
        text-align: right !important;
      }
      
      /* NADPISY */
      h1, h2, h3, h4, h5, h6 {
        page-break-after: avoid !important;
        page-break-inside: avoid !important;
        margin: 6pt 0 3pt 0 !important;
        font-weight: bold !important;
        color: #c00 !important;
      }
      
      h2 {
        font-size: 12pt !important;
        margin-top: 0 !important;
      }
      
      h3 {
        font-size: 10pt !important;
        margin: 5pt 0 3pt 0 !important;
      }
      
      h3.es-report-title {
        font-size: 11pt !important;
        margin-bottom: 6pt !important;
      }
      
      /* ODDĚLOVAČE */
      .hr-line-dashed {
        border: none !important;
        border-top: 1px dashed #999 !important;
        margin: 8pt 0 !important;
        background: transparent !important;
        height: 0 !important;
        page-break-after: avoid !important;
      }
      
      /* OBRÁZKY */
      img {
        max-width: 100% !important;
        height: auto !important;
        page-break-inside: avoid !important;
        display: block !important;
      }
      
      /* SUB A SUP */
      sub, sup {
        font-size: 70% !important;
        line-height: 0 !important;
        position: relative !important;
        vertical-align: baseline !important;
      }
      
      sup {
        top: -0.5em !important;
      }
      
      sub {
        bottom: -0.25em !important;
      }
      
      /* SKRYTÉ PRVKY */
      .no-print,
      .btn,
      button,
      nav,
      .navbar,
      .sidebar,
      .modal,
      .es-report-sidebar,
      #pageBreadcrumb,
      .footer,
      .slimScrollDiv {
        display: none !important;
        visibility: hidden !important;
      }
      
      /* Manuální zalomení */
      .page-break {
        page-break-before: always !important;
        break-before: page !important;
      }
      
      .page-break-after {
        page-break-after: always !important;
        break-after: page !important;
      }
      
      .no-break {
        page-break-inside: avoid !important;
        break-inside: avoid !important;
      }
    }
  `;
  
  const styleElement = document.createElement('style');
  styleElement.id = 'dynamic-print-css';
  styleElement.textContent = printCSS;
  document.head.appendChild(styleElement);
  
  console.log('✅ Print CSS načteno!');
  console.log('');
  console.log('🎯 NYNÍ:');
  console.log('   1. Stiskni Ctrl+P');
  console.log('   2. Ulož jako PDF');
  console.log('   3. Layout by měl být zachován');
  
  const printButton = document.createElement('button');
  printButton.textContent = '🖨️ Tisknout';
  printButton.className = 'no-print';
  printButton.style.cssText = `
    position: fixed;
    top: 80px;
    right: 20px;
    padding: 12px 24px;
    background: #1ab394;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    z-index: 999999;
    transition: all 0.3s;
  `;
  
  printButton.onmouseenter = () => {
    printButton.style.background = '#17a689';
    printButton.style.transform = 'translateY(-2px)';
  };
  
  printButton.onmouseleave = () => {
    printButton.style.background = '#1ab394';
    printButton.style.transform = 'translateY(0)';
  };
  
  printButton.onclick = () => window.print();
  
  document.body.appendChild(printButton);
  
})();