# -using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using OpenQA.Selenium;

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        IWebDriver Browser;
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            Browser.Navigate().GoToUrl("http://google.com ");
            IWebElement SearchInput = Browser.FindElement(By.Id("lst-ib"));
            SearchInput.SendKeys("Вконтакте" + OpenQA.Selenium.Keys.Enter);
        }

        private void button2_Click(object sender, EventArgs e)
        {
            Browser.Quit();
        }

        private void button4_Click(object sender, EventArgs e)
        {
            OpenQA.Selenium.Chrome.ChromeOptions со = new OpenQA.Selenium.Chrome.ChromeOptions();
            со.AddArgument(@"user-data-derwc:\Users\Appdata\Local\Google\Chrome\User Data");
            Browser = new OpenQA.Selenium.Chrome.ChromeDriver(со);
            Browser.Manage().Window.Maximize();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            IWebElement element = Browser.FindElement(By.Id("text"));
            element.SendKeys("Тест");
        }

        private void button5_Click(object sender, EventArgs e)
        {
            List<IWebElement> News = Browser.FindElements(By.CssSelector("#tabnews_newsc a")).ToList();

            for (int i = 0; i < News.Count; i++ )
            {
                string s = News[i].Text;

                if (s.StartsWith("ФСБ"))
                {
                    textBox1.AppendText("Новость №" + (i + 1).ToString() + "Начинается с текста 'ФСБ'"+"\r\n");
                }
                if(s.StartsWith("Кремля"))
                {
                    textBox1.AppendText("Новость №" + (i + 1).ToString() + "заканчивается текстом 'Кремля'" +"\r\n");
                }
                if (s.Contains("Вывести"))
                {
                    textBox1.AppendText("Новость №" + (i + 1).ToString() + "содержит текст 'вывести'" + "\r\n");
                    News[i].Click();
                    break;
