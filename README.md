<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Semana 11A — Room · Android Studio + Kotlin</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Raleway:wght@300;600;800;900&family=Lora:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0f1e;
    --surface: #0f1628;
    --surface2: #151d35;
    --border: #1e2a4a;
    --border2: #253358;
    --accent: #3b82f6;
    --accent2: #10b981;
    --accent3: #f59e0b;
    --accent4: #ef4444;
    --text: #e2e8f0;
    --text-dim: #94a3b8;
    --text-muted: #475569;
    --kotlin: #b08fff;
    --xml: #fb923c;
    --gradle: #10b981;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: 'Lora', serif; font-weight: 400; line-height: 1.75; }

  /* ── HERO ── */
  .hero {
    background: linear-gradient(160deg, #0a0f1e 0%, #0d1530 60%, #0a1525 100%);
    padding: 56px 48px 48px;
    border-bottom: 1px solid var(--border2);
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute;
    top: -100px; left: -100px;
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(59,130,246,0.08) 0%, transparent 65%);
    pointer-events: none;
  }
  .hero::after {
    content: 'ROOM';
    position: absolute;
    right: -20px; bottom: -30px;
    font-family: 'Raleway', sans-serif;
    font-size: 200px;
    font-weight: 900;
    color: rgba(59,130,246,0.04);
    line-height: 1;
    pointer-events: none;
    user-select: none;
  }

  .week-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    border: 1px solid rgba(59,130,246,0.35);
    background: rgba(59,130,246,0.08);
    color: #93c5fd;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    padding: 5px 14px;
    border-radius: 20px;
    margin-bottom: 20px;
    width: fit-content;
  }
  .hero h1 {
    font-family: 'Raleway', sans-serif;
    font-size: clamp(2.4rem, 6vw, 4rem);
    font-weight: 900;
    color: #fff;
    line-height: 1.05;
    margin-bottom: 8px;
    letter-spacing: -0.01em;
  }
  .hero h1 span { color: #60a5fa; }
  .hero-sub { color: #64748b; font-size: 1rem; max-width: 600px; margin-bottom: 32px; font-family: 'Lora', serif; }
  .meta-strip { display: flex; flex-wrap: wrap; gap: 20px; border-top: 1px solid var(--border); padding-top: 24px; }
  .meta-chip { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: #475569; display: flex; align-items: center; gap: 6px; }
  .meta-chip strong { color: #94a3b8; font-weight: 600; }

  .container { max-width: 980px; margin: 0 auto; padding: 0 28px 100px; }

  /* ── CLASE HEADER ── */
  .clase-header { margin: 60px 0 28px; display: flex; align-items: center; gap: 20px; }
  .clase-badge {
    font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700;
    letter-spacing: 0.14em; text-transform: uppercase;
    background: var(--accent); color: #fff;
    padding: 5px 14px; border-radius: 3px; white-space: nowrap; flex-shrink: 0;
  }
  .clase-title { font-family: 'Raleway', sans-serif; font-size: 1.7rem; font-weight: 800; color: var(--text); line-height: 1.15; }
  .clase-title span { color: var(--accent); }
  .clase-line { flex: 1; height: 1px; background: var(--border); }

  /* ── OBJETIVO ── */
  .objetivo {
    background: rgba(16,185,129,0.06); border: 1px solid rgba(16,185,129,0.2);
    border-left: 4px solid var(--accent2); border-radius: 6px;
    padding: 14px 20px; margin-bottom: 28px; font-size: 0.9rem;
  }
  .objetivo strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent2); display: block; margin-bottom: 5px; }
  .objetivo p { margin: 0; color: var(--text-dim); font-family: 'Lora', serif; }

  /* ── SECTION ── */
  .section { margin-bottom: 36px; }
  .section-title { font-family: 'Raleway', sans-serif; font-size: 0.9rem; font-weight: 800; color: var(--text); margin-bottom: 14px; display: flex; align-items: center; gap: 10px; text-transform: uppercase; letter-spacing: 0.07em; }
  .section-title .tag { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; padding: 2px 8px; border-radius: 3px; }
  .section-title .tag.kotlin { background: rgba(176,143,255,0.2); color: var(--kotlin); border: 1px solid rgba(176,143,255,0.3); }
  .section-title .tag.xml    { background: rgba(251,146,60,0.2);  color: var(--xml);    border: 1px solid rgba(251,146,60,0.3); }
  .section-title .tag.gradle { background: rgba(16,185,129,0.2);  color: var(--gradle); border: 1px solid rgba(16,185,129,0.3); }
  .section-title .tag.concept{ background: rgba(59,130,246,0.2);  color: #93c5fd;       border: 1px solid rgba(59,130,246,0.3); }

  p { margin-bottom: 12px; color: var(--text-dim); font-size: 0.93rem; font-family: 'Lora', serif; }

  /* ── ROOM ARCHITECTURE DIAGRAM ── */
  .room-arch {
    background: var(--surface);
    border: 1px solid var(--border2);
    border-radius: 10px;
    padding: 28px;
    margin: 20px 0;
    display: flex;
    flex-direction: column;
    gap: 12px;
  }
  .arch-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px; font-weight: 700; letter-spacing: 0.14em;
    text-transform: uppercase; color: var(--text-muted); margin-bottom: 4px;
  }
  .arch-row { display: flex; gap: 8px; align-items: stretch; }
  .arch-box {
    flex: 1; border-radius: 8px; padding: 14px 16px;
    font-family: 'JetBrains Mono', monospace; font-size: 12px;
  }
  .arch-box h4 { font-size: 0.85rem; font-weight: 700; margin-bottom: 4px; }
  .arch-box p { font-size: 0.75rem; margin: 0; font-family: 'JetBrains Mono', monospace; }
  .box-entity  { background: rgba(59,130,246,0.12); border: 1px solid rgba(59,130,246,0.25); }
  .box-entity  h4, .box-entity p { color: #93c5fd; }
  .box-dao     { background: rgba(16,185,129,0.12); border: 1px solid rgba(16,185,129,0.25); }
  .box-dao     h4, .box-dao p { color: #6ee7b7; }
  .box-db      { background: rgba(245,158,11,0.12); border: 1px solid rgba(245,158,11,0.25); }
  .box-db      h4, .box-db p { color: #fcd34d; }
  .arch-arrow  { display: flex; align-items: center; padding: 0 4px; color: var(--text-muted); font-size: 18px; }
  .arch-divider { height: 1px; background: var(--border); margin: 4px 0; }

  /* ── CONCEPTS ── */
  .concepts { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; margin: 18px 0; }
  .concept-card { background: var(--surface); border: 1px solid var(--border); border-radius: 8px; padding: 16px; border-top: 3px solid var(--accent); }
  .concept-card.green  { border-top-color: var(--accent2); }
  .concept-card.yellow { border-top-color: var(--accent3); }
  .concept-card .icon  { font-size: 1.3rem; margin-bottom: 8px; }
  .concept-card h4     { font-family: 'JetBrains Mono', monospace; font-size: 0.78rem; color: var(--accent); margin-bottom: 5px; font-weight: 700; }
  .concept-card.green h4  { color: var(--accent2); }
  .concept-card.yellow h4 { color: var(--accent3); }
  .concept-card p { font-size: 0.82rem; margin: 0; font-family: 'Lora', serif; }

  /* ── CODE BLOCK ── */
  .code-block { background: #060b18; border: 1px solid var(--border2); border-radius: 8px; overflow: hidden; margin: 16px 0; font-size: 0.84rem; }
  .code-header { display: flex; align-items: center; justify-content: space-between; padding: 9px 16px; background: var(--surface2); border-bottom: 1px solid var(--border); }
  .code-lang { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; padding: 2px 9px; border-radius: 3px; }
  .lang-kotlin { background: rgba(176,143,255,0.15); color: var(--kotlin); border: 1px solid rgba(176,143,255,0.3); }
  .lang-xml    { background: rgba(251,146,60,0.15);  color: var(--xml);    border: 1px solid rgba(251,146,60,0.3); }
  .lang-gradle { background: rgba(16,185,129,0.15);  color: var(--gradle); border: 1px solid rgba(16,185,129,0.3); }
  .code-filename { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--text-muted); }
  .code-body { padding: 18px 20px; overflow-x: auto; }
  pre { font-family: 'JetBrains Mono', monospace; line-height: 1.65; white-space: pre; color: #cbd5e1; background: transparent; }
  .kw  { color: #c792ea; } .fn  { color: #82aaff; } .str { color: #c3e88d; }
  .cm  { color: #2d3f5e; font-style: italic; } .num { color: #f78c6c; }
  .cls { color: #ffcb6b; } .op  { color: #89ddff; } .tag { color: #e06c75; }
  .attr{ color: #c3e88d; } .val { color: #f78c6c; } .an  { color: #89ddff; }

  /* ── ALERT ── */
  .alert { border-radius: 6px; padding: 13px 17px; margin: 14px 0; font-size: 0.87rem; display: flex; gap: 12px; align-items: flex-start; }
  .alert-blue   { background: rgba(59,130,246,0.07);  border: 1px solid rgba(59,130,246,0.2); }
  .alert-green  { background: rgba(16,185,129,0.07);  border: 1px solid rgba(16,185,129,0.2); }
  .alert-yellow { background: rgba(245,158,11,0.07);  border: 1px solid rgba(245,158,11,0.2); }
  .alert-red    { background: rgba(239,68,68,0.07);   border: 1px solid rgba(239,68,68,0.2); }
  .alert-icon   { font-size: 1.1rem; flex-shrink: 0; margin-top: 1px; }
  .alert p      { margin: 0; color: var(--text-dim); font-family: 'Lora', serif; }

  /* ── DIVIDER ── */
  .divider { margin: 56px 0 0; border: none; border-top: 1px solid var(--border2); position: relative; }
  .divider::after { content: 'CLASE 02'; position: absolute; top: -10px; left: 50%; transform: translateX(-50%); background: var(--bg); padding: 0 14px; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; color: var(--text-muted); }

  /* ── TAREA ── */
  .tarea { background: var(--surface); border: 1px solid var(--border2); border-top: 4px solid var(--accent); border-radius: 10px; padding: 34px; margin-top: 56px; }
  .tarea-badge { display: inline-block; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; padding: 4px 12px; border-radius: 3px; margin-bottom: 14px; }
  .tarea h2 { font-family: 'Raleway', sans-serif; font-size: 1.8rem; font-weight: 900; color: var(--text); margin-bottom: 10px; }
  .tarea-desc { color: var(--text-dim); margin-bottom: 22px; font-size: 0.93rem; }
  .reqs { display: flex; flex-direction: column; gap: 10px; margin-bottom: 22px; }
  .req { display: flex; gap: 12px; align-items: flex-start; font-size: 0.89rem; color: var(--text-dim); font-family: 'Lora', serif; }
  .req-num { min-width: 22px; height: 22px; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 10px; font-weight: 700; border-radius: 3px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }
  .req-num.star { background: var(--accent2); }
  .entrega { background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; padding: 13px 17px; font-size: 0.84rem; }
  .entrega strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--accent3); text-transform: uppercase; letter-spacing: 0.12em; display: block; margin-bottom: 4px; }
  .entrega p { color: var(--text-muted); margin: 0; font-family: 'Lora', serif; }

  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: var(--surface); }
  ::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }
</style>
</head>
<body>

<div class="hero">
  <div class="week-tag">📅 Semana 11 de 16 · Opción A</div>
  <h1>Room<br><span>Base de Datos Local</span></h1>
  <p class="hero-sub">Persiste datos en SQLite de forma limpia y segura usando Room: la librería de persistencia oficial de Android que integra perfectamente con ViewModel y LiveData.</p>
  <div class="meta-strip">
    <div class="meta-chip">Clases <strong>2 × 2 hrs</strong></div>
    <div class="meta-chip">Lenguaje <strong>Kotlin</strong></div>
    <div class="meta-chip">Layout <strong>ConstraintLayout</strong></div>
    <div class="meta-chip">Prereq <strong>Semana 10 — ViewModel + LiveData</strong></div>
  </div>
</div>

<div class="container">

  <!-- ══════════════ CLASE 1 ══════════════ -->
  <div class="clase-header">
    <span class="clase-badge">Clase 01</span>
    <div class="clase-title">Entidad, DAO y <span>Database</span></div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Entender los tres componentes de Room, configurar la base de datos y realizar las operaciones CRUD básicas (Create, Read, Update, Delete).</p>
  </div>

  <div class="section">
    <div class="section-title"><span class="tag concept">CONCEPTO</span> Los 3 componentes de Room</div>
    <p>Room es una capa de abstracción sobre SQLite. En lugar de escribir SQL a mano y manejar cursores, defines clases Kotlin con anotaciones y Room genera todo el código de acceso a datos.</p>

    <div class="room-arch">
      <div class="arch-label">// Arquitectura completa de Room</div>
      <div class="arch-row">
        <div class="arch-box box-entity">
          <h4>@Entity</h4>
          <p>Clase de datos = tabla SQL.<br>Cada propiedad = columna.</p>
        </div>
        <div class="arch-arrow">→</div>
        <div class="arch-box box-dao">
          <h4>@Dao</h4>
          <p>Interface con @Query, @Insert,<br>@Update, @Delete.</p>
        </div>
        <div class="arch-arrow">→</div>
        <div class="arch-box box-db">
          <h4>@Database</h4>
          <p>Clase abstracta. Punto de<br>entrada a la base de datos.</p>
        </div>
      </div>
      <div class="arch-divider"></div>
      <div class="arch-row">
        <div class="arch-box box-entity" style="flex:0 0 auto; padding: 10px 14px;">
          <p style="font-size:0.7rem">data class Nota(<br>  @PrimaryKey val id: Int,<br>  val titulo: String<br>)</p>
        </div>
        <div class="arch-arrow">→</div>
        <div class="arch-box box-dao" style="flex:0 0 auto; padding: 10px 14px;">
          <p style="font-size:0.7rem">@Query("SELECT * FROM nota")<br>fun getAll(): LiveData&lt;List&lt;Nota&gt;&gt;<br>@Insert fun insertar(nota: Nota)</p>
        </div>
        <div class="arch-arrow">→</div>
        <div class="arch-box box-db" style="flex:0 0 auto; padding: 10px 14px;">
          <p style="font-size:0.7rem">abstract fun notaDao(): NotaDao<br><br>companion object { ... }</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Código 1: build.gradle -->
  <div class="section">
    <div class="section-title"><span class="tag gradle">GRADLE</span> Código 1 — Dependencias</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-gradle">Gradle · Kotlin DSL</span>
        <span class="code-filename">build.gradle.kts (Module)</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">plugins</span> {
    <span class="cm">// Necesario para que Room genere el código con kapt</span>
    id(<span class="str">"kotlin-kapt"</span>)
}

<span class="fn">dependencies</span> {
    <span class="cm">// Room</span>
    <span class="kw">val</span> roomVersion = <span class="str">"2.6.1"</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.room:room-runtime:$roomVersion"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.room:room-ktx:$roomVersion"</span>)     <span class="cm">// coroutines + Flow</span>
    <span class="fn">kapt</span>(<span class="str">"androidx.room:room-compiler:$roomVersion"</span>)

    <span class="cm">// ViewModel + LiveData (de la Semana 10)</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-livedata-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.activity:activity-ktx:1.9.0"</span>)
}</pre></div>
    </div>
    <div class="alert alert-yellow">
      <span class="alert-icon">⚠️</span>
      <p><strong>kapt</strong> es el procesador de anotaciones de Kotlin. Sin él, Room no puede generar el código SQL en tiempo de compilación. El plugin <code>kotlin-kapt</code> debe estar en el bloque <code>plugins{}</code> del módulo, no del proyecto raíz.</p>
    </div>
  </div>

  <!-- Código 2: Nota.kt @Entity -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 2 — Nota.kt (@Entity)</div>
    <p>La anotación <code>@Entity</code> convierte esta data class en una tabla SQL. Cada instancia de <code>Nota</code> es una fila.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">Nota.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.room.Entity
<span class="kw">import</span> androidx.room.PrimaryKey

<span class="an">@Entity</span>(tableName = <span class="str">"notas"</span>)          <span class="cm">// nombre de la tabla en SQLite</span>
<span class="kw">data class</span> <span class="cls">Nota</span>(
    <span class="an">@PrimaryKey</span>(autoGenerate = <span class="kw">true</span>)  <span class="cm">// Room genera el ID automáticamente</span>
    <span class="kw">val</span> id:        <span class="cls">Int</span> = <span class="num">0</span>,
    <span class="kw">val</span> titulo:    <span class="cls">String</span>,
    <span class="kw">val</span> contenido: <span class="cls">String</span>,
    <span class="kw">val</span> fechaMs:   <span class="cls">Long</span> = <span class="cls">System</span>.<span class="fn">currentTimeMillis</span>()
)</pre></div>
    </div>
  </div>

  <!-- Código 3: NotaDao.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 3 — NotaDao.kt (@Dao)</div>
    <p>El DAO (Data Access Object) define todas las operaciones disponibles sobre la tabla. Room implementa esta interface automáticamente en compilación.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaDao.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.room.*

<span class="an">@Dao</span>
<span class="kw">interface</span> <span class="cls">NotaDao</span> {

    <span class="cm">// LiveData como retorno: Room actualiza la lista automáticamente
    // cuando la tabla cambia. No necesitamos consultar manualmente.</span>
    <span class="an">@Query</span>(<span class="str">"SELECT * FROM notas ORDER BY fechaMs DESC"</span>)
    <span class="kw">fun</span> <span class="fn">getAll</span>(): <span class="cls">LiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;&gt;

    <span class="an">@Query</span>(<span class="str">"SELECT * FROM notas WHERE id = :notaId"</span>)
    <span class="kw">fun</span> <span class="fn">getById</span>(notaId: <span class="cls">Int</span>): <span class="cls">LiveData</span>&lt;<span class="cls">Nota</span>?&gt;

    <span class="cm">// suspend: estas operaciones NO pueden correr en el hilo principal</span>
    <span class="an">@Insert</span>
    <span class="kw">suspend fun</span> <span class="fn">insertar</span>(nota: <span class="cls">Nota</span>)

    <span class="an">@Update</span>
    <span class="kw">suspend fun</span> <span class="fn">actualizar</span>(nota: <span class="cls">Nota</span>)

    <span class="an">@Delete</span>
    <span class="kw">suspend fun</span> <span class="fn">eliminar</span>(nota: <span class="cls">Nota</span>)

    <span class="an">@Query</span>(<span class="str">"DELETE FROM notas"</span>)
    <span class="kw">suspend fun</span> <span class="fn">eliminarTodas</span>()
}</pre></div>
    </div>
    <div class="alert alert-blue">
      <span class="alert-icon">💡</span>
      <p><strong>suspend vs LiveData:</strong> Las funciones de escritura (<code>@Insert</code>, <code>@Update</code>, <code>@Delete</code>) son <code>suspend</code> porque modifican la base de datos y no pueden bloquearse en el hilo principal. Las de lectura retornan <code>LiveData</code>, que Room actualiza automáticamente en background.</p>
    </div>
  </div>

  <!-- Código 4: AppDatabase.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 4 — AppDatabase.kt (@Database)</div>
    <p>La clase Database es el punto de entrada a toda la base de datos. Debe ser un Singleton — solo debe existir una instancia en toda la app.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">AppDatabase.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.content.Context
<span class="kw">import</span> androidx.room.Database
<span class="kw">import</span> androidx.room.Room
<span class="kw">import</span> androidx.room.RoomDatabase

<span class="an">@Database</span>(
    entities = [<span class="cls">Nota</span>::<span class="kw">class</span>],   <span class="cm">// lista de todas las @Entity</span>
    version  = <span class="num">1</span>,               <span class="cm">// incrementar si cambias el esquema</span>
    exportSchema = <span class="kw">false</span>
)
<span class="kw">abstract class</span> <span class="cls">AppDatabase</span> : <span class="cls">RoomDatabase</span>() {

    <span class="cm">// Room implementa este método — nosotros solo lo declaramos</span>
    <span class="kw">abstract fun</span> <span class="fn">notaDao</span>(): <span class="cls">NotaDao</span>

    <span class="kw">companion object</span> {
        <span class="an">@Volatile</span>  <span class="cm">// garantiza visibilidad entre hilos</span>
        <span class="kw">private var</span> INSTANCE: <span class="cls">AppDatabase</span>? = <span class="kw">null</span>

        <span class="kw">fun</span> <span class="fn">getDatabase</span>(context: <span class="cls">Context</span>): <span class="cls">AppDatabase</span> {
            <span class="cm">// synchronized: evita que dos hilos creen instancias simultáneamente</span>
            <span class="kw">return</span> INSTANCE <span class="op">?:</span> <span class="kw">synchronized</span>(<span class="kw">this</span>) {
                <span class="kw">val</span> instance = <span class="cls">Room</span>.<span class="fn">databaseBuilder</span>(
                    context.applicationContext,
                    <span class="cls">AppDatabase</span>::<span class="kw">class</span>.java,
                    <span class="str">"app_database"</span>
                ).<span class="fn">build</span>()
                INSTANCE = instance
                instance
            }
        }
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 5: AndroidManifest -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 5 — AndroidManifest.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">AndroidManifest.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;manifest</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag">&gt;</span>
    <span class="tag">&lt;application</span>
        <span class="attr">android:allowBackup</span>=<span class="val">"true"</span>
        <span class="attr">android:theme</span>=<span class="val">"@style/Theme.AppCompat.Light.DarkActionBar"</span><span class="tag">&gt;</span>

        <span class="tag">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".NotasActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"true"</span><span class="tag">&gt;</span>
            <span class="tag">&lt;intent-filter&gt;</span>
                <span class="tag">&lt;action</span> <span class="attr">android:name</span>=<span class="val">"android.intent.action.MAIN"</span> <span class="tag">/&gt;</span>
                <span class="tag">&lt;category</span> <span class="attr">android:name</span>=<span class="val">"android.intent.category.LAUNCHER"</span> <span class="tag">/&gt;</span>
            <span class="tag">&lt;/intent-filter&gt;</span>
        <span class="tag">&lt;/activity&gt;</span>

        <span class="tag">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".EditarNotaActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"false"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;/application&gt;</span>
<span class="tag">&lt;/manifest&gt;</span></pre></div>
    </div>
  </div>

  <!-- ══════════════ CLASE 2 ══════════════ -->
  <hr class="divider">

  <div class="clase-header" style="margin-top:56px">
    <span class="clase-badge">Clase 02</span>
    <div class="clase-title">Repository, ViewModel y <span>UI completa</span></div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Conectar Room con ViewModel a través del patrón Repository. Construir la UI completa con RecyclerView para listar notas y una segunda Activity para crear y editar.</p>
  </div>

  <!-- Código 6: NotaRepository -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 6 — NotaRepository.kt</div>
    <p>El Repository es la capa intermedia entre el ViewModel y el DAO. El ViewModel no debe conocer la fuente de datos — solo el Repository.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaRepository.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData

<span class="kw">class</span> <span class="cls">NotaRepository</span>(<span class="kw">private val</span> dao: <span class="cls">NotaDao</span>) {

    <span class="cm">// LiveData fluye directo del DAO — Room maneja el hilo</span>
    <span class="kw">val</span> todasLasNotas: <span class="cls">LiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;&gt; = dao.<span class="fn">getAll</span>()

    <span class="cm">// Las operaciones de escritura son suspend — se llaman desde una coroutine</span>
    <span class="kw">suspend fun</span> <span class="fn">insertar</span>(nota: <span class="cls">Nota</span>) = dao.<span class="fn">insertar</span>(nota)
    <span class="kw">suspend fun</span> <span class="fn">actualizar</span>(nota: <span class="cls">Nota</span>) = dao.<span class="fn">actualizar</span>(nota)
    <span class="kw">suspend fun</span> <span class="fn">eliminar</span>(nota: <span class="cls">Nota</span>)   = dao.<span class="fn">eliminar</span>(nota)
}</pre></div>
    </div>
  </div>

  <!-- Código 7: NotaViewModel -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 7 — NotaViewModel.kt</div>
    <p>El ViewModel usa <code>viewModelScope</code> para lanzar coroutines — cuando el ViewModel se destruye, las coroutines se cancelan automáticamente.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaViewModel.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.app.Application
<span class="kw">import</span> androidx.lifecycle.AndroidViewModel
<span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.lifecycle.viewModelScope
<span class="kw">import</span> kotlinx.coroutines.launch

<span class="cm">// AndroidViewModel recibe el Application — necesario para crear la DB</span>
<span class="kw">class</span> <span class="cls">NotaViewModel</span>(application: <span class="cls">Application</span>) : <span class="cls">AndroidViewModel</span>(application) {

    <span class="kw">private val</span> repository: <span class="cls">NotaRepository</span>

    <span class="kw">val</span> todasLasNotas: <span class="cls">LiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;&gt;

    <span class="kw">init</span> {
        <span class="kw">val</span> dao = <span class="cls">AppDatabase</span>.<span class="fn">getDatabase</span>(application).<span class="fn">notaDao</span>()
        repository = <span class="cls">NotaRepository</span>(dao)
        todasLasNotas = repository.todasLasNotas
    }

    <span class="cm">// viewModelScope: coroutine ligada al ciclo de vida del ViewModel</span>
    <span class="kw">fun</span> <span class="fn">insertar</span>(nota: <span class="cls">Nota</span>) = viewModelScope.<span class="fn">launch</span> {
        repository.<span class="fn">insertar</span>(nota)
    }

    <span class="kw">fun</span> <span class="fn">actualizar</span>(nota: <span class="cls">Nota</span>) = viewModelScope.<span class="fn">launch</span> {
        repository.<span class="fn">actualizar</span>(nota)
    }

    <span class="kw">fun</span> <span class="fn">eliminar</span>(nota: <span class="cls">Nota</span>) = viewModelScope.<span class="fn">launch</span> {
        repository.<span class="fn">eliminar</span>(nota)
    }
}</pre></div>
    </div>
    <div class="alert alert-blue">
      <span class="alert-icon">💡</span>
      <p><strong>AndroidViewModel vs ViewModel:</strong> Se usa <code>AndroidViewModel</code> cuando se necesita el contexto de la Application (por ejemplo para construir la base de datos). Nunca se debe pasar una Activity o Fragment como contexto al ViewModel — causaría un memory leak.</p>
    </div>
  </div>

  <!-- Código 8: activity_notas.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 8 — activity_notas.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_notas.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;androidx.recyclerview.widget.RecyclerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/recyclerNotas"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:clipToPadding</span>=<span class="val">"false"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;com.google.android.material.floatingactionbutton.FloatingActionButton</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/fabNuevaNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_margin</span>=<span class="val">"24dp"</span>
        <span class="attr">android:src</span>=<span class="val">"@android:drawable/ic_input_add"</span>
        <span class="attr">android:contentDescription</span>=<span class="val">"Nueva nota"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 9: item_nota.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 9 — item_nota.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/item_nota.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
    <span class="attr">android:padding</span>=<span class="val">"14dp"</span>
    <span class="attr">android:background</span>=<span class="val">"?attr/selectableItemBackground"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvTituloNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"17sp"</span>
        <span class="attr">android:textStyle</span>=<span class="val">"bold"</span>
        <span class="attr">android:maxLines</span>=<span class="val">"1"</span>
        <span class="attr">android:ellipsize</span>=<span class="val">"end"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toStartOf</span>=<span class="val">"@id/btnEliminarNota"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvContenidoNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:textSize</span>=<span class="val">"13sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#888"</span>
        <span class="attr">android:maxLines</span>=<span class="val">"2"</span>
        <span class="attr">android:ellipsize</span>=<span class="val">"end"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"4dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvTituloNota"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toStartOf</span>=<span class="val">"@id/btnEliminarNota"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnEliminarNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"🗑"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 10: NotaAdapter.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 10 — NotaAdapter.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaAdapter.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> android.view.LayoutInflater
<span class="kw">import</span> android.view.View
<span class="kw">import</span> android.view.ViewGroup
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView

<span class="kw">class</span> <span class="cls">NotaAdapter</span>(
    <span class="kw">private var</span> notas: <span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt; = <span class="fn">emptyList</span>(),
    <span class="kw">private val</span> onClick:   (<span class="cls">Nota</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>,
    <span class="kw">private val</span> onEliminar: (<span class="cls">Nota</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>
) : <span class="cls">RecyclerView</span>.<span class="cls">Adapter</span>&lt;<span class="cls">NotaAdapter</span>.<span class="cls">NotaViewHolder</span>&gt;() {

    <span class="kw">inner class</span> <span class="cls">NotaViewHolder</span>(itemView: <span class="cls">View</span>) : <span class="cls">RecyclerView</span>.<span class="cls">ViewHolder</span>(itemView) {
        <span class="kw">val</span> tvTitulo:   <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvTituloNota)
        <span class="kw">val</span> tvCont:     <span class="cls">TextView</span> = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.tvContenidoNota)
        <span class="kw">val</span> btnElim:    <span class="cls">Button</span>   = itemView.<span class="fn">findViewById</span>(<span class="cls">R</span>.id.btnEliminarNota)
    }

    <span class="kw">override fun</span> <span class="fn">onCreateViewHolder</span>(parent: <span class="cls">ViewGroup</span>, viewType: <span class="cls">Int</span>) =
        <span class="cls">NotaViewHolder</span>(<span class="cls">LayoutInflater</span>.<span class="fn">from</span>(parent.context)
            .<span class="fn">inflate</span>(<span class="cls">R</span>.layout.item_nota, parent, <span class="kw">false</span>))

    <span class="kw">override fun</span> <span class="fn">onBindViewHolder</span>(holder: <span class="cls">NotaViewHolder</span>, position: <span class="cls">Int</span>) {
        <span class="kw">val</span> nota = notas[position]
        holder.tvTitulo.text = nota.titulo
        holder.tvCont.text   = nota.contenido
        holder.itemView.<span class="fn">setOnClickListener</span> { <span class="fn">onClick</span>(nota) }
        holder.btnElim.<span class="fn">setOnClickListener</span>  { <span class="fn">onEliminar</span>(nota) }
    }

    <span class="kw">override fun</span> <span class="fn">getItemCount</span>() = notas.size

    <span class="kw">fun</span> <span class="fn">actualizarLista</span>(nuevas: <span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;) {
        notas = nuevas
        <span class="fn">notifyDataSetChanged</span>()
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 11: NotasActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 11 — NotasActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotasActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> androidx.activity.viewModels
<span class="kw">import</span> androidx.activity.result.contract.ActivityResultContracts
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView
<span class="kw">import</span> com.google.android.material.floatingactionbutton.FloatingActionButton

<span class="kw">class</span> <span class="cls">NotasActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">private val</span> viewModel: <span class="cls">NotaViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="cm">// Launcher para crear o editar una nota (Semana 8)</span>
    <span class="kw">private val</span> editarLauncher = <span class="fn">registerForActivityResult</span>(
        <span class="cls">ActivityResultContracts</span>.<span class="cls">StartActivityForResult</span>()
    ) { result <span class="op">-&gt;</span>
        <span class="kw">if</span> (result.resultCode == <span class="cls">RESULT_OK</span>) {
            <span class="kw">val</span> titulo    = result.data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"TITULO"</span>)    <span class="op">?:</span> <span class="kw">return</span><span class="an">@registerForActivityResult</span>
            <span class="kw">val</span> contenido = result.data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"CONTENIDO"</span>) <span class="op">?:</span> <span class="str">""</span>
            <span class="kw">val</span> id        = result.data<span class="op">?.</span><span class="fn">getIntExtra</span>(<span class="str">"ID"</span>, -<span class="num">1</span>) <span class="op">?:</span> -<span class="num">1</span>

            <span class="kw">if</span> (id == -<span class="num">1</span>) {
                <span class="cm">// Nota nueva</span>
                viewModel.<span class="fn">insertar</span>(<span class="cls">Nota</span>(titulo = titulo, contenido = contenido))
            } <span class="kw">else</span> {
                <span class="cm">// Nota editada</span>
                viewModel.<span class="fn">actualizar</span>(<span class="cls">Nota</span>(id = id, titulo = titulo, contenido = contenido))
            }
        }
    }

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_notas)

        <span class="kw">val</span> adapter = <span class="cls">NotaAdapter</span>(
            onClick    = { nota <span class="op">-&gt;</span> <span class="fn">abrirEditor</span>(nota) },
            onEliminar = { nota <span class="op">-&gt;</span> viewModel.<span class="fn">eliminar</span>(nota) }
        )

        <span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerNotas).<span class="fn">apply</span> {
            layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="kw">this</span><span class="an">@NotasActivity</span>)
            this.adapter  = adapter
        }

        <span class="cm">// El observer recibe la lista fresca de Room automáticamente</span>
        viewModel.todasLasNotas.<span class="fn">observe</span>(<span class="kw">this</span>) { lista <span class="op">-&gt;</span>
            adapter.<span class="fn">actualizarLista</span>(lista)
        }

        <span class="fn">findViewById</span>&lt;<span class="cls">FloatingActionButton</span>&gt;(<span class="cls">R</span>.id.fabNuevaNota).<span class="fn">setOnClickListener</span> {
            <span class="fn">abrirEditor</span>(<span class="kw">null</span>)
        }
    }

    <span class="kw">private fun</span> <span class="fn">abrirEditor</span>(nota: <span class="cls">Nota</span>?) {
        <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">EditarNotaActivity</span>::<span class="kw">class</span>.java)
        nota<span class="op">?.</span><span class="fn">let</span> {
            intent.<span class="fn">putExtra</span>(<span class="str">"ID"</span>,        it.id)
            intent.<span class="fn">putExtra</span>(<span class="str">"TITULO"</span>,    it.titulo)
            intent.<span class="fn">putExtra</span>(<span class="str">"CONTENIDO"</span>, it.contenido)
        }
        editarLauncher.<span class="fn">launch</span>(intent)
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 12: activity_editar_nota.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 12 — activity_editar_nota.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_editar_nota.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:padding</span>=<span class="val">"20dp"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;EditText</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/etTituloNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:hint</span>=<span class="val">"Título"</span>
        <span class="attr">android:textSize</span>=<span class="val">"20sp"</span>
        <span class="attr">android:inputType</span>=<span class="val">"textCapSentences"</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;EditText</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/etContenidoNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:hint</span>=<span class="val">"Escribe tu nota aquí..."</span>
        <span class="attr">android:gravity</span>=<span class="val">"top"</span>
        <span class="attr">android:inputType</span>=<span class="val">"textMultiLine|textCapSentences"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/etTituloNota"</span>
        <span class="attr">app:layout_constraintBottom_toTopOf</span>=<span class="val">"@id/btnGuardarNota"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;Button</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/btnGuardarNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:text</span>=<span class="val">"Guardar"</span>
        <span class="attr">android:layout_marginTop</span>=<span class="val">"12dp"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 13: EditarNotaActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 13 — EditarNotaActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">EditarNotaActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.app.Activity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.EditText

<span class="kw">class</span> <span class="cls">EditarNotaActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_editar_nota)

        <span class="kw">val</span> etTitulo   = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etTituloNota)
        <span class="kw">val</span> etContenido = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etContenidoNota)
        <span class="kw">val</span> btnGuardar  = <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnGuardarNota)

        <span class="cm">// Si vienen extras, es edición — prellenar los campos</span>
        <span class="kw">val</span> idExistente = intent.<span class="fn">getIntExtra</span>(<span class="str">"ID"</span>, -<span class="num">1</span>)
        intent.<span class="fn">getStringExtra</span>(<span class="str">"TITULO"</span>)<span class="op">?.</span><span class="fn">let</span> { etTitulo.<span class="fn">setText</span>(it) }
        intent.<span class="fn">getStringExtra</span>(<span class="str">"CONTENIDO"</span>)<span class="op">?.</span><span class="fn">let</span> { etContenido.<span class="fn">setText</span>(it) }

        btnGuardar.<span class="fn">setOnClickListener</span> {
            <span class="kw">val</span> titulo = etTitulo.text.toString().<span class="fn">trim</span>()
            <span class="kw">if</span> (titulo.<span class="fn">isEmpty</span>()) {
                etTitulo.error = <span class="str">"El título no puede estar vacío"</span>
                <span class="kw">return</span><span class="an">@setOnClickListener</span>
            }
            <span class="kw">val</span> resultado = android.content.<span class="cls">Intent</span>()
            resultado.<span class="fn">putExtra</span>(<span class="str">"TITULO"</span>,    titulo)
            resultado.<span class="fn">putExtra</span>(<span class="str">"CONTENIDO"</span>, etContenido.text.toString())
            resultado.<span class="fn">putExtra</span>(<span class="str">"ID"</span>,        idExistente)
            <span class="fn">setResult</span>(<span class="cls">Activity</span>.RESULT_OK, resultado)
            <span class="fn">finish</span>()
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-green">
      <span class="alert-icon">🔗</span>
      <p><strong>Integración total:</strong> Esta app usa RecyclerView (Semana 7), ActivityResultLauncher (Semana 8), ViewModel + LiveData (Semana 10) y Room (Semana 11) trabajando juntos. Es el primer ejemplo que integra todas las capas de una arquitectura Android real.</p>
    </div>
  </div>

  <!-- TAREA -->
  <div class="tarea">
    <div class="tarea-badge">📝 Práctica — Tarea</div>
    <h2>App: Inventario Personal</h2>
    <p class="tarea-desc">Construye una app de inventario que persista datos localmente con Room, integrando todo lo visto desde la Semana 7.</p>
    <div class="reqs">
      <div class="req"><div class="req-num">1</div><div>Crear una <strong>@Entity <code>Producto</code></strong> con: id (autoGenerate), nombre, cantidad (Int), precio (Double) y categoria (String).</div></div>
      <div class="req"><div class="req-num">2</div><div>Crear el <strong>@Dao</strong> con: <code>getAll()</code> retornando <code>LiveData</code>, <code>getByCategoria(cat: String)</code>, <code>insertar</code>, <code>actualizar</code> y <code>eliminar</code> como <code>suspend fun</code>.</div></div>
      <div class="req"><div class="req-num">3</div><div>Implementar el patrón completo: <strong>@Database → Repository → ViewModel → Activity</strong>. El ViewModel debe ser <code>AndroidViewModel</code>.</div></div>
      <div class="req"><div class="req-num">4</div><div>La UI muestra un <strong>RecyclerView</strong> con los productos y un <strong>FAB</strong> para agregar. Al hacer clic en un ítem se abre la Activity de edición con los datos precargados.</div></div>
      <div class="req"><div class="req-num">5</div><div>Agregar un <strong>Spinner</strong> o botones de filtro para mostrar solo los productos de una categoría, usando una <code>@Query</code> con parámetro en el DAO.</div></div>
      <div class="req"><div class="req-num star">⭐</div><div><strong>Punto extra:</strong> Agregar en el DAO una <code>@Query</code> que retorne el total de productos y el valor total del inventario (suma de cantidad × precio), y mostrarlo en un TextView de resumen.</div></div>
    </div>
    <div class="entrega">
      <strong>📦 Entrega</strong>
      <p>Proyecto en .zip. Verificar que al cerrar y reabrir la app los datos persisten.</p>
    </div>
  </div>

</div>
</body>
</html>
