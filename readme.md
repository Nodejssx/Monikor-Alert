<h1 dir="auto">Haqaqq Grafana Monitor Kuruslum Rehberis</h1>
<h2 dir="auto"><a id="user-content-&ouml;nkoşullar" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#%C3%B6nko%C5%9Fullar" aria-hidden="true"></a>&Ouml;nkoşullar</h2>
<h3 dir="auto"><a id="user-content-nodeunuzun-kurulu-olduğunu-sunucuya-exporter-y&uuml;kleyin" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#nodeunuzun-kurulu-oldu%C4%9Funu-sunucuya-exporter-y%C3%BCkleyin" aria-hidden="true"></a>Node'unuzun kurulu olduğunu sunucuya&nbsp;<code>exporter</code>&nbsp;y&uuml;kleyin.</h3>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto">
<pre class="notranslate"><code>wget -O NodeistorExporter.sh https://raw.githubusercontent.com/Nodeist/Nodeistor/main/NodeistorExporter &amp;&amp; chmod +x NodeistorExporter.sh &amp;&amp; ./NodeistorExporter.sh
</code></pre>
</div>
<p dir="auto">Kurulum sırasında sizden bir ka&ccedil; bilgi istenecek. Bunlar:</p>
<table>
<thead>
<tr>
<th>ANAHTAR</th>
<th>DEĞER</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>bond_denom</strong></td>
<td>Denom Degeri. &Ouml;rneğin Haqq i&ccedil;in&nbsp;<code>aISLM</code></td>
</tr>
<tr>
<td><strong>bench_prefix</strong></td>
<td>Bench Prefix Değeri. &Ouml;rneğin Haqq i&ccedil;in&nbsp;<code>haqq</code>. Bu değeri c&uuml;zdan adresinizden &ouml;ğrenebilirsiniz.&nbsp;<strong>Haqq</strong>1r5g0kes6jutsydez9qw2tx6vuc8scpxn5qtyle</td>
</tr>
<tr>
<td><strong>grpc_port</strong></td>
<td>"app.toml" dosyasında tanımlanan doğrulayıcı "grpc" bağlantı noktanız. Varsayılan değer&nbsp;<code>29090</code>dır</td>
</tr>
<tr>
<td><strong>rpc_port</strong></td>
<td>"config.toml" dosyasında tanımlanan doğrulayıcı "rpc" bağlantı noktanız. Varsayılan değer&nbsp;<code>29657</code>dir</td>
</tr>
</tbody>
</table>
<p dir="auto">Sunucuzda aşağıdaki portların a&ccedil;ık olduğundan emin olun:</p>
<ul dir="auto">
<li><code>9100</code>&nbsp;(node-exporter)</li>
<li><code>9300</code>&nbsp;(cosmos-exporter)</li>
</ul>
<h2 dir="auto"><a id="user-content-grafana-monit&ouml;r-kurulumu" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#grafana-monit%C3%B6r-kurulumu" aria-hidden="true"></a>Grafana Monit&ouml;r Kurulumu</h2>
<p dir="auto">Doğrulayıcınızı doğru şekilde takip ve analiz edebilmeniz i&ccedil;in grafana monit&ouml;r&uuml; ayrı bir sunucuya kurmanızı &ouml;neririz. Node'unuz durursa, sunucunuz arızalanırsa vs. gibi durumlarda da verileri takip etme şansınız olur. &Ccedil;ok b&uuml;y&uuml;k bir sistem gereksinimi istemiyor. aşağıdaki &ouml;zelliklerde bir sistem monit&ouml;r i&ccedil;in yeterli.</p>
<h3 dir="auto"><a id="user-content-sistem-gereksinimleri" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#sistem-gereksinimleri" aria-hidden="true"></a>Sistem Gereksinimleri</h3>
<p dir="auto">Ubuntu 20.04 / 1 VCPU / 2 GB RAM / 20 GB SSD</p>
<h3 dir="auto"><a id="user-content-monit&ouml;r-kurulumu" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#monit%C3%B6r-kurulumu" aria-hidden="true"></a>Monit&ouml;r Kurulumu</h3>
<p dir="auto">Yeni sunucunuza aşağıdaki kodu yazarak monit&ouml;r kurulumunu tamamlayabilirsiniz.</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto">
<pre class="notranslate"><code>wget -O NodeistMonitor.sh https://raw.githubusercontent.com/Nodeist/Nodeistor/main/NodeistMonitor &amp;&amp; chmod +x NodeistMonitor.sh &amp;&amp; ./NodeistMonitor.sh
</code></pre>
</div>
<h3 dir="auto"><a id="user-content-prometheus-konfigurasyon-dosyasına-doğrulayıcı-ekleme" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#prometheus-konfigurasyon-dosyas%C4%B1na-do%C4%9Frulay%C4%B1c%C4%B1-ekleme" aria-hidden="true"></a>Prometheus Konfigurasyon dosyasına doğrulayıcı ekleme.</h3>
<p dir="auto">Aşağıdaki kodu farklı ağlar i&ccedil;in birden &ccedil;ok kere kullanabilirsiniz. Yani aynı monit&ouml;rde birden fazla validat&ouml;r&uuml;n istatistiğini g&ouml;r&uuml;nt&uuml;leyebilirsiniz. Bunu yapabilmek i&ccedil;in eklemek istediğiniz her ağ i&ccedil;in aşağıdaki kodu revize ederek yazın.</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto">
<pre class="notranslate"><code>$HOME/Nodeistor/ag_ekle.sh VALIDATOR_IP WALLET_ADDRESS VALOPER_ADDRESS PROJECT_NAME
</code></pre>
</div>
<blockquote>
<p dir="auto">&Ouml;rneğin:&nbsp;<code>$HOME/Nodeistor/ag_ekle.sh 1.2.3.4 seivaloper1s9rtstp8amx9vgsekhf3rk4rdr7qvg8dlxuy8v sei1s9rtstp8amx9vgsekhf3rk4rdr7qvg8d6jg3tl sei</code></p>
</blockquote>
<h3 dir="auto"><a id="user-content-dockeri-başlatın" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#dockeri-ba%C5%9Flat%C4%B1n" aria-hidden="true"></a>Dockeri Başlatın</h3>
<p dir="auto">Monitor dağıtımına başlayın.</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto">
<pre class="notranslate"><code>cd $HOME/Nodeistor &amp;&amp; docker compose up -d
</code></pre>
</div>
<p dir="auto">Kullanılan portlar:</p>
<ul dir="auto">
<li><code>9090</code>&nbsp;(prometheus)</li>
<li><code>9999</code>&nbsp;(grafana)</li>
</ul>
<h2 dir="auto"><a id="user-content-ayarlar" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#ayarlar" aria-hidden="true"></a>Ayarlar</h2>
<h3 dir="auto"><a id="user-content-grafana-konfig&uuml;rasyonu" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#grafana-konfig%C3%BCrasyonu" aria-hidden="true"></a>Grafana konfig&uuml;rasyonu</h3>
<ol dir="auto">
<li>Web tarayıcınızı a&ccedil;ın ve&nbsp;<code>sunucuipadresiniz:9999</code>&nbsp;yazarak grafana aray&uuml;z&uuml;ne ulaşın.</li>
</ol>
<p dir="auto"><a href="https://camo.githubusercontent.com/b746d33c968a395ed0cd68cba5e6a0ee74fe35c8bb42baadc5fa745d8d3a84e3/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f713576317278672e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/b746d33c968a395ed0cd68cba5e6a0ee74fe35c8bb42baadc5fa745d8d3a84e3/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f713576317278672e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/q5v1rxg.png" /></a></p>
<ol dir="auto" start="2">
<li>
<p dir="auto">Kullanıcı adınız ve şifreniz&nbsp;<code>admin</code>. ilk girişten sonra şifrenizi g&uuml;ncellemeniz istenecektir.</p>
</li>
<li>
<p dir="auto">Nodeistor'u import edin.</p>
</li>
</ol>
<p dir="auto">3.1. Sol men&uuml;den&nbsp;<code>+</code>&nbsp;iconuna basın ve a&ccedil;ılan pencereden&nbsp;<code>Import</code>&nbsp;se&ccedil;eneğine tıklayın.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/d44dca967f9167a46190f7436ab6004bebf0e0f873264e88e80a345f9ab8564b/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f673736736b766d2e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/d44dca967f9167a46190f7436ab6004bebf0e0f873264e88e80a345f9ab8564b/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f673736736b766d2e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/g76skvm.png" /></a></p>
<p dir="auto">3.2. grafana.com Kontrol paneli kimliğini yazın&nbsp;<code>16580</code>. Ve&nbsp;<code>Load</code>&nbsp;a basın.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/446eb0da262f0fb5211dcd88e29a39b6068750a4bffb0e6e3c53904e12b1b47c/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f326334656c79382e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/446eb0da262f0fb5211dcd88e29a39b6068750a4bffb0e6e3c53904e12b1b47c/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f326334656c79382e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/2c4ely8.png" /></a></p>
<p dir="auto">3.3. Veri kaynağı olarak prometheus'u se&ccedil;in ve importa basın.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/3177a1017e29de9b6afbe7878086f80f0e86741c0a58add8cbad75e0ddae867e/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f616368756564652e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/3177a1017e29de9b6afbe7878086f80f0e86741c0a58add8cbad75e0ddae867e/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f616368756564652e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/achuede.png" /></a></p>
<ol dir="auto" start="4">
<li>Explorer yapılandırması</li>
</ol>
<p dir="auto">Normalde en &ccedil;ok blok ka&ccedil;ıranlar paneli nodes.guru explorer'a g&ouml;re uyarlıdır.</p>
<p dir="auto">Eğer nodes.guru explorer'da olmayan bir ağ eklemek isterseniz en &ccedil;ok blok ka&ccedil;ıranlar sekmesinde d&uuml;zenleme yapmanız gerekir.</p>
<blockquote>
<p dir="auto">Bu işlem sadece&nbsp;<code>En &ccedil;ok blok ka&ccedil;ıranlar</code>&nbsp;sekmesi i&ccedil;in ge&ccedil;erlidir ve &ccedil;ok da şart değildir.</p>
</blockquote>
<p dir="auto">Sekme başlığına tıklayın ve&nbsp;<code>edit</code>e basın.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/b6fab11e29593e489c028b7f933220dc2759e88d062b4a7a98f4bfc99d3116bf/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f376737307372622e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/b6fab11e29593e489c028b7f933220dc2759e88d062b4a7a98f4bfc99d3116bf/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f376737307372622e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/7g70srb.png" /></a></p>
<p dir="auto">4.1.&nbsp;<strong>Overrides</strong>&nbsp;sekmesine gelin.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/c11194fe54e7eb726abc49c8c765d5ae7ca4db42a6347e14d8ff4212d6697521/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f616264616839302e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/c11194fe54e7eb726abc49c8c765d5ae7ca4db42a6347e14d8ff4212d6697521/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f616264616839302e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/abdah90.png" /></a></p>
<p dir="auto">4.2.&nbsp;<strong>datalink</strong>&nbsp;b&ouml;l&uuml;m&uuml;nden d&uuml;zenle butonuna basın.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/ecc110cf103aecbdb0e4d9556edb649614f6a5c0f790e7384638f077cce92a6f/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f6770716f7961682e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/ecc110cf103aecbdb0e4d9556edb649614f6a5c0f790e7384638f077cce92a6f/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f6770716f7961682e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/gpqoyah.png" /></a></p>
<p dir="auto">4.3 Explorer adresini g&uuml;ncelleyin ve&nbsp;<strong>Save</strong>&nbsp;butonuna basın.</p>
<p dir="auto"><a href="https://camo.githubusercontent.com/f7f2cda8c46551b0256ee632c16879b9083eeaefc74a98782137ead8fcc60e72/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f6231737434786e2e706e67" target="_blank" rel="noopener noreferrer nofollow"><img src="https://camo.githubusercontent.com/f7f2cda8c46551b0256ee632c16879b9083eeaefc74a98782137ead8fcc60e72/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f6231737434786e2e706e67" alt="image" data-canonical-src="https://i.hizliresim.com/b1st4xn.png" /></a></p>
<p dir="auto">4.4. Son olarak sağ &uuml;st k&ouml;şeden tekrar&nbsp;<strong>Save</strong>&nbsp;butonuna basın ve ardından&nbsp;<strong>Apply</strong>&nbsp;butonuna basarak uygulayın.</p>
<ol dir="auto" start="5">
<li>Tebrikler! Nodeistor'u başarıyla kurdunuz ve yapılandırdınız.</li>
</ol>
<h2 dir="auto"><a id="user-content-pano-i&ccedil;eriği" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#pano-i%C3%A7eri%C4%9Fi" aria-hidden="true"></a>Pano i&ccedil;eriği</h2>
<p dir="auto">Grafana panosu 4 b&ouml;l&uuml;me ayrılmıştır:</p>
<ul dir="auto">
<li><strong>Doğrulayıcı sağlığı</strong>&nbsp;- doğrulayıcı sağlığı i&ccedil;in ana istatistikler. bağlı eşler ve cevapsız bloklar</li>
<li><strong>Zincir sağlığı</strong>&nbsp;- zincir sağlığı istatistiklerinin &ouml;zeti ve en iyi doğrulayıcıların eksik blokları listesi</li>
<li><strong>Doğrulayıcı istatistikleri</strong>&nbsp;- r&uuml;tbe, sınırlı jetonlar, komisyon, delegasyonlar ve &ouml;d&uuml;ller gibi doğrulayıcı hakkında bilgiler</li>
<li><strong>Donanım sağlığı</strong>&nbsp;- sistem donanım &ouml;l&ccedil;&uuml;mleri. işlemci, ram, ağ kullanımı</li>
</ul>
<h2 dir="auto"><a id="user-content-i̇statistikleri-sıfırlayın" class="anchor" href="https://github.com/Nodeist/Kurulumlar/tree/main/Haqq/Monitor#i%CC%87statistikleri-s%C4%B1f%C4%B1rlay%C4%B1n" aria-hidden="true"></a>İstatistikleri Sıfırlayın</h2>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto">
<pre class="notranslate"><code>cd $HOME/Nodeistor
docker compose down
</code></pre>
</div>
