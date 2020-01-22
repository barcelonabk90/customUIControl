# customUIControl
namespace CustomControl
{
    partial class ColorBorderTextbox
    {
        /// <summary> 
        /// Required designer variable.
        /// </summary>
        private System.ComponentModel.IContainer components = null;

        /// <summary> 
        /// Clean up any resources being used.
        /// </summary>
        /// <param name="disposing">true if managed resources should be disposed; otherwise, false.</param>
        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
            {
                components.Dispose();
            }
            base.Dispose(disposing);
        }

        #region Component Designer generated code

        /// <summary> 
        /// Required method for Designer support - do not modify 
        /// the contents of this method with the code editor.
        /// </summary>
        private void InitializeComponent()
        {
            this.textBox = new System.Windows.Forms.TextBox();
            this.SuspendLayout();
            // 
            // textBox
            // 
            this.textBox.BorderStyle = System.Windows.Forms.BorderStyle.None;
            this.textBox.Location = new System.Drawing.Point(1, 1);
            this.textBox.Multiline = true;
            this.textBox.Name = "textBox";
            this.textBox.Size = new System.Drawing.Size(98, 18);
            this.textBox.TabIndex = 0;
            this.textBox.Enter += new System.EventHandler(this.textBox_Enter);
            this.textBox.Leave += new System.EventHandler(this.textBox_Leave);
            // 
            // ColorBorderTextbox
            // 
            this.AutoScaleDimensions = new System.Drawing.SizeF(6F, 13F);
            this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
            this.Controls.Add(this.textBox);
            this.Name = "ColorBorderTextbox";
            this.Size = new System.Drawing.Size(100, 20);
            this.Paint += new System.Windows.Forms.PaintEventHandler(this.ColorBorderTextbox_Paint);
            this.ResumeLayout(false);
            this.PerformLayout();

        }

        #endregion

        private System.Windows.Forms.TextBox textBox;
    }
}

using System;
using System.Drawing;
using System.Windows.Forms;

namespace CustomControl
{
    public partial class ColorBorderTextbox : UserControl
    {
        Color m_BorderColor = Color.Red;
        Color m_BorderColor_Def = Color.Blue;
        Boolean m_BorderTop = true;
        Boolean m_BorderBottom = true;
        Boolean m_BorderLeft = true;
        Boolean m_BorderRight = true;

        /// <summary>
        /// Set Border's Color
        /// </summary>
        public Color BorderColor
        {
            set { m_BorderColor = value; _RedrawBorder(m_BorderColor); }
            get { return m_BorderColor; }
        }

        /// <summary>
        /// Set Default Border's Color
        /// </summary>
        public Color BorderColorDefault
        {
            set { m_BorderColor_Def = value; _RedrawBorder(m_BorderColor_Def); }
            get { return m_BorderColor_Def; }
        }

        /// <summary>
        /// Show/Hide Border Top
        /// </summary>
        public Boolean BorderTop
        {
            set { m_BorderTop = value; _RedrawBorder(m_BorderColor); }
            get { return m_BorderTop; }
        }

        /// <summary>
        /// Show/Hide Border Bottom
        /// </summary>
        public Boolean BorderBottom
        {
            set { m_BorderBottom = value; _RedrawBorder(m_BorderColor); }
            get { return m_BorderBottom; }
        }

        /// <summary>
        /// Show/Hide Border Left
        /// </summary>
        public Boolean BorderLeft
        {
            set { m_BorderLeft = value; _RedrawBorder(m_BorderColor); }
            get { return m_BorderLeft; }
        }

        /// <summary>
        /// Show/Hide Border Right
        /// </summary>
        public Boolean BorderRight
        {
            set { m_BorderRight = value; _RedrawBorder(m_BorderColor); }
            get { return m_BorderRight; }
        }

        public ColorBorderTextbox()
        {
            InitializeComponent();
        }

        private void ColorBorderTextbox_Paint(object sender, PaintEventArgs e)
        {
            _ResizeTextbox();

            _RedrawBorder(m_BorderColor_Def);
        }

        private void textBox_Enter(object sender, EventArgs e)
        {
            _RedrawBorder(m_BorderColor);
        }

        private void textBox_Leave(object sender, EventArgs e)
        {
            _RedrawBorder(m_BorderColor_Def);
        }

        private void _ResizeTextbox()
        {
            Int32 width;
            Int32 height;

            width = this.Width - 2;
            height = this.Height - 2;

            this.textBox.Size = new Size(width, height);
        }

        private void _RedrawBorder(Color aColor)
        {
            Graphics g = this.CreateGraphics();
            Pen pen;
            int r = this.ClientRectangle.Right - 1;
            int b = this.ClientRectangle.Bottom - 1;
            pen = new Pen(aColor);
            if (m_BorderTop == true) g.DrawLine(pen, 0, 0, r, 0); // 上
            if (m_BorderLeft == true) g.DrawLine(pen, 0, 0, 0, b); // 左
            if (m_BorderRight == true) g.DrawLine(pen, r, 0, r, b); // 右
            if (m_BorderBottom == true) g.DrawLine(pen, 0, b, r, b); // 下
        }
    }
}
