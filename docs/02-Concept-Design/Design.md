---
title: Concept Generation and Design Ideation
---

## Component Selection

This decision matrix shows the tradeoffs we evaluated when selecting the motor and wheel combination for the project.

<div class="pdfjs-viewer" data-pdf="../static/314-component-selection.pdf" style="border: 1px solid #d0d7de; border-radius: 8px; overflow: hidden; background: #f6f8fa; margin: 1rem 0;">
  <div style="display: flex; align-items: center; justify-content: space-between; gap: 0.75rem; padding: 0.75rem 1rem; background: #eef2f7; border-bottom: 1px solid #d0d7de;">
    <strong>Component Selection PDF</strong>
    <div style="display: flex; gap: 0.5rem;">
      <button class="pdf-prev" type="button">Previous</button>
      <button class="pdf-next" type="button">Next</button>
      <a href="../static/314-component-selection.pdf" target="_blank" rel="noopener">Open PDF</a>
    </div>
  </div>
  <div style="padding: 1rem; text-align: center; background: #ffffff;">
    <canvas class="pdf-canvas" style="max-width: 100%; height: auto; border: 1px solid #d0d7de; background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.08);"></canvas>
  </div>
  <div style="padding: 0.5rem 1rem 1rem; text-align: center; font-size: 0.9rem; color: #4b5563;">
    <span class="pdf-page-label">Page 1</span>
  </div>
</div>

*The PDF is rendered directly in the page so you can review the full selection matrix without leaving the site.*

The selected option was the most cost-effective solution that still satisfied the required torque and wheel compatibility constraints. This made it the strongest balance of performance, availability, and manufacturability for the prototype.

## Bill of Materials

The bill of materials summarizes the selected parts and their quantities for the design.

<div class="pdfjs-viewer" data-pdf="../static/bill-of-materials.pdf" style="border: 1px solid #d0d7de; border-radius: 8px; overflow: hidden; background: #f6f8fa; margin: 1rem 0;">
  <div style="display: flex; align-items: center; justify-content: space-between; gap: 0.75rem; padding: 0.75rem 1rem; background: #eef2f7; border-bottom: 1px solid #d0d7de;">
    <strong>Bill of Materials PDF</strong>
    <div style="display: flex; gap: 0.5rem;">
      <button class="pdf-prev" type="button">Previous</button>
      <button class="pdf-next" type="button">Next</button>
      <a href="../static/bill-of-materials.pdf" target="_blank" rel="noopener">Open PDF</a>
    </div>
  </div>
  <div style="padding: 1rem; text-align: center; background: #ffffff;">
    <canvas class="pdf-canvas" style="max-width: 100%; height: auto; border: 1px solid #d0d7de; background: white; box-shadow: 0 2px 8px rgba(0,0,0,0.08);"></canvas>
  </div>
  <div style="padding: 0.5rem 1rem 1rem; text-align: center; font-size: 0.9rem; color: #4b5563;">
    <span class="pdf-page-label">Page 1</span>
  </div>
</div>

*The PDF is rendered directly in the page so you can review the full bill of materials without leaving the site.*

<script type="module">
  import * as pdfjsLib from 'https://cdn.jsdelivr.net/npm/pdfjs-dist@4.10.38/+esm';
  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdn.jsdelivr.net/npm/pdfjs-dist@4.10.38/build/pdf.worker.min.mjs';

  const viewers = document.querySelectorAll('.pdfjs-viewer');

  viewers.forEach((viewer) => {
    const pdfUrl = viewer.dataset.pdf;
    const canvas = viewer.querySelector('.pdf-canvas');
    const prevButton = viewer.querySelector('.pdf-prev');
    const nextButton = viewer.querySelector('.pdf-next');
    const pageLabel = viewer.querySelector('.pdf-page-label');

    let pdfDoc = null;
    let pageNum = 1;

    function renderPage() {
      if (!pdfDoc) return;

      pdfDoc.getPage(pageNum).then((page) => {
        const viewport = page.getViewport({ scale: 1.3 });
        const context = canvas.getContext('2d');
        canvas.width = viewport.width;
        canvas.height = viewport.height;
        canvas.style.width = '100%';
        canvas.style.height = 'auto';

        const renderContext = {
          canvasContext: context,
          viewport: viewport
        };

        page.render(renderContext).promise.then(() => {
          pageLabel.textContent = `Page ${pageNum} of ${pdfDoc.numPages}`;
        });
      });
    }

    pdfjsLib.getDocument(pdfUrl).promise.then((pdf) => {
      pdfDoc = pdf;
      renderPage();
    }).catch(() => {
      pageLabel.textContent = 'PDF could not be displayed in the browser. Use the Open PDF link above.';
      canvas.replaceWith(document.createTextNode('PDF preview unavailable.'));
    });

    prevButton.addEventListener('click', () => {
      if (pdfDoc && pageNum > 1) {
        pageNum -= 1;
        renderPage();
      }
    });

    nextButton.addEventListener('click', () => {
      if (pdfDoc && pageNum < pdfDoc.numPages) {
        pageNum += 1;
        renderPage();
      }
    });
  });
</script>