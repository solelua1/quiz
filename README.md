# quiz
Meu primeiro projeto no guit

using System;
using System.Drawing;
using System.Threading;
using System.Windows.Forms;

namespace ButtonClickBlinkExample
{
    public partial class Form1 : Form
    {
        private bool isBlinking = false;
        private Color defaultColor = Color.Blue;
        private Color blinkColor = Color.Yellow;

        public Form1()
        {
            InitializeComponent();
        }

        private void btnBlink_Click(object sender, EventArgs e)
        {
            if (!isBlinking)
            {
                isBlinking = true;
                // Inicia uma nova thread para realizar o brilho
                Thread blinkThread = new Thread(BlinkButton);
                blinkThread.Start();
            }
        }

        private void BlinkButton()
        {
            while (isBlinking)
            {
                // Alterna a cor do botão
                btnBlink.Invoke((MethodInvoker)delegate
                {
                    if (btnBlink.BackColor == defaultColor)
                        btnBlink.BackColor = blinkColor;
                    else
                        btnBlink.BackColor = defaultColor;
                });

                // Aguarda um pequeno intervalo
                Thread.Sleep(500);
            }

            // Restaura a cor padrão do botão
            btnBlink.Invoke((MethodInvoker)delegate
            {
                btnBlink.BackColor = defaultColor;
            });
        }
    }
}


