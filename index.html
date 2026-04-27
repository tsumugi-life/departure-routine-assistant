import React, { useEffect, useMemo, useState } from "react";


const EVENT_THEME = {
  学校: { card: "bg-slate-100 border-slate-300", soft: "bg-slate-200", icon: "🏫" },
  フラ: { card: "bg-rose-50 border-rose-200", soft: "bg-rose-100", icon: "🌺" },
  通院: { card: "bg-emerald-50 border-emerald-200", soft: "bg-emerald-100", icon: "🏥" },
  買い物: { card: "bg-stone-100 border-stone-300", soft: "bg-stone-200", icon: "🛒" },
  習い事: { card: "bg-indigo-50 border-indigo-200", soft: "bg-indigo-100", icon: "📚" },
  default: { card: "bg-stone-50 border-stone-200", soft: "bg-stone-100", icon: "🗓️" },
};

const getTheme = (title) => EVENT_THEME[title] || EVENT_THEME.default;
const toMinutes = (time) => {
  const [h, m] = time.split(":").map(Number);
  return h * 60 + m;
};
const minutesUntil = (time, now) => toMinutes(time) - (now.getHours() * 60 + now.getMinutes());
const formatUntil = (mins) => {
  if (mins < 0) return "出発時刻を過ぎています";
  if (mins < 60) return `出発まで${mins}分`;
  const h = Math.floor(mins / 60);
  const m = mins % 60;
  return m === 0 ? `あと${h}時間` : `あと${h}時間${m}分`;
};

export default function DepartureRoutineAssistantV2() {
  const [activeScreen, setActiveScreen] = useState("check");
  const [now, setNow] = useState(new Date());
  const [dailyItems, setDailyItems] = useState(["鍵", "スマホ", "財布"]);
  const [templates, setTemplates] = useState([
    { id: "school", name: "学校セット", items: ["筆箱", "ノート", "水筒"] },
    { id: "hula", name: "フラセット", items: ["パウ", "水筒", "ノート"] },
    { id: "hospital", name: "通院セット", items: ["診察券", "保険証", "お薬手帳"] },
    { id: "shopping", name: "買い物セット", items: ["エコバッグ", "ポイントカード"] },
  ]);
  const [events, setEvents] = useState([
    { id: 1, title: "学校", time: "08:00", icon: "🏫", templateId: "school", specialItems: ["申込書"], checked: false,  },
    { id: 2, title: "フラ", time: "17:30", icon: "🌺", templateId: "hula", specialItems: [], checked: false,  },
    { id: 3, title: "通院", time: "19:00", icon: "🏥", templateId: "hospital", specialItems: ["保険証"], checked: false,  },
  ]);
  const [eventNameOptions, setEventNameOptions] = useState([
    { name: "学校", icon: "🏫" },
    { name: "フラ", icon: "🌺" },
    { name: "通院", icon: "🏥" },
    { name: "買い物", icon: "🛒" },
    { name: "習い事", icon: "📚" },
  ]);
  const [quickItems, setQuickItems] = useState(["申込書", "保険証", "レインコート", "水筒"]);
  const [templateExclusions, setTemplateExclusions] = useState({});
  const [selectedEventId, setSelectedEventId] = useState(1);
  const [confirmIndex, setConfirmIndex] = useState(0);
  const [completed, setCompleted] = useState(false);
  const [notYetMessage, setNotYetMessage] = useState(false);
  const [voiceEnabled, setVoiceEnabled] = useState(true);
  const [prepReminderEnabled, setPrepReminderEnabled] = useState(true);
  const [prepReminderTime, setPrepReminderTime] = useState("23:00");
  const [prepDoneToday, setPrepDoneToday] = useState(false);

  useEffect(() => {
    const timer = setInterval(() => setNow(new Date()), 1000);
    return () => clearInterval(timer);
  }, []);

    const visibleEvents = useMemo(
    () => events.slice().sort((a,b)=>toMinutes(a.time)-toMinutes(b.time)),
    [events]
  );
  const nextEvent = useMemo(() => {
    const upcoming = visibleEvents.find((event) => minutesUntil(event.time, now) >= 0 && !event.checked);
    return upcoming || visibleEvents.find((event) => minutesUntil(event.time, now) >= 0) || visibleEvents[0] || events[0];
  }, [visibleEvents, now, events]);
  const selectedEvent = events.find((event) => event.id === selectedEventId) || nextEvent;
  const selectedTemplate = templates.find((template) => template.id === selectedEvent?.templateId);
  const confirmItems = useMemo(() => {
    const excluded = templateExclusions[selectedEvent?.id] || [];
    const templateItems = (selectedTemplate?.items || []).filter((item) => !excluded.includes(item));
    return [
      ...(selectedEvent?.specialItems || []).map((name) => ({ name, category: "今日だけ" })),
      ...templateItems.map((name) => ({ name, category: selectedTemplate?.name || "シーン別セット" })),
      ...dailyItems.map((name) => ({ name, category: "毎日" })),
    ].filter((item) => item.name?.trim());
  }, [selectedEvent, selectedTemplate, dailyItems, templateExclusions]);

  const canSpeak = typeof window !== "undefined" && "speechSynthesis" in window;
  const speakText = (text) => {
    if (!voiceEnabled || !canSpeak || !text) return;
    window.speechSynthesis.cancel();
    const utterance = new SpeechSynthesisUtterance(text);
    utterance.lang = "ja-JP";
    utterance.rate = 0.9;
    window.speechSynthesis.speak(utterance);
  };
  const buildSpeechText = (item) => item?.category === "今日だけ"
    ? `今日は特別な持ち物があります。${item.name}です。もう一度確認します。${item.name}。`
    : `${item?.name || ""}、持った？`;

  useEffect(() => {
    if (activeScreen === "confirm" && confirmItems[confirmIndex] && !completed) {
      const timer = setTimeout(() => speakText(buildSpeechText(confirmItems[confirmIndex])), 250);
      return () => clearTimeout(timer);
    }
  }, [activeScreen, confirmIndex, completed, selectedEventId, voiceEnabled]);

  useEffect(() => {
    if (activeScreen === "confirm" && completed) {
      const timer = setTimeout(() => speakText("出発確認完了です。いってらっしゃい。"), 250);
      return () => clearTimeout(timer);
    }
  }, [activeScreen, completed, voiceEnabled]);

  const changeScreen = (screen) => {
    if (canSpeak) window.speechSynthesis.cancel();
    setActiveScreen(screen);
  };
  const updateEvent = (id, field, value) => setEvents((prev) => prev.map((e) => (e.id === id ? { ...e, [field]: value } : e)));
  const startConfirmation = (eventId) => {
    if (canSpeak) window.speechSynthesis.cancel();
    setSelectedEventId(eventId || selectedEventId);
    setConfirmIndex(0);
    setCompleted(false);
    setNotYetMessage(false);
    setActiveScreen("confirm");
  };
  const addEvent = (data) => {
    const newEvent = {
      id: Date.now(),
      title: data.title,
      time: data.time,
      icon: data.icon || getTheme(data.title).icon,
      templateId: data.templateId || templates[0]?.id,
      specialItems: [],
      checked: false,
    };
    setEvents((prev) => [...prev, newEvent]);
    if (!eventNameOptions.some((opt) => opt.name === data.title)) {
      setEventNameOptions((prev) => [...prev.slice(0, 4), { name: data.title, icon: newEvent.icon }]);
    }
  };
  const duplicateEvent = (event) => addEvent({ ...event, title: `${event.title}コピー` });
  const removeEvent = (id) => setEvents((prev) => prev.filter((event) => event.id !== id));
  const addTemplate = () => setTemplates((prev) => [...prev, { id: `template-${Date.now()}`, name: "新しいセット", items: ["新しい持ち物"] }]);
  const updateTemplate = (id, field, value) => setTemplates((prev) => prev.map((t) => (t.id === id ? { ...t, [field]: value } : t)));
  const addTemplateItem = (id) => setTemplates((prev) => prev.map((t) => (t.id === id ? { ...t, items: [...t.items, "新しい持ち物"] } : t)));
  const updateTemplateItem = (id, index, value) => setTemplates((prev) => prev.map((t) => (t.id === id ? { ...t, items: t.items.map((item, i) => (i === index ? value : item)) } : t)));
  const removeTemplateItem = (id, index) => setTemplates((prev) => prev.map((t) => (t.id === id ? { ...t, items: t.items.filter((_, i) => i !== index) } : t)));
  const removeTemplate = (id) => setTemplates((prev) => prev.filter((t) => t.id !== id));

  const progress = confirmItems.length ? Math.round(((completed ? confirmItems.length : confirmIndex) / confirmItems.length) * 100) : 0;

  return (
    <div className="min-h-screen bg-[#f7f3ec] text-stone-800 flex justify-center">
      <div className="w-full max-w-md min-h-screen bg-[#fbf8f2] shadow-xl relative pb-24">
        <header className="px-5 pt-6 pb-4 sticky top-0 bg-[#fbf8f2]/95 backdrop-blur z-10 border-b border-stone-100">
          
          <h1 className="text-2xl font-bold tracking-tight">出発ルーティン・アシスタント</h1>
          <div className="mt-3 text-center text-sm font-bold text-stone-500">明日の準備 → 確認開始 → 出発</div>
          <div className="mt-4 rounded-[1.5rem] bg-white p-4 border border-stone-100 shadow-sm text-center">
            <div className="text-lg font-bold">{now.getFullYear()}年 {now.getMonth() + 1}月{now.getDate()}日（{now.toLocaleDateString("ja-JP", { weekday: "short" }).replace("曜", "")}）</div>
            <div className="text-4xl font-black mt-2 tracking-tight font-mono">{now.toLocaleTimeString("ja-JP", { hour: "2-digit", minute: "2-digit", second: "2-digit" })}</div>
          </div>
        </header>

        <main className="px-5 py-5 space-y-5">
          {activeScreen === "check" && <HomeDashboard nextEvent={nextEvent} events={visibleEvents} now={now} templates={templates} onStart={startConfirmation} />}
          {activeScreen === "prep" && (
            <PrepScreen
              setPrepDoneToday={setPrepDoneToday}
              events={events}
              templates={templates}
              updateEvent={updateEvent}
              addEvent={addEvent}
              duplicateEvent={duplicateEvent}
              removeEvent={removeEvent}
              startConfirmation={startConfirmation}
              eventNameOptions={eventNameOptions}
              setEventNameOptions={setEventNameOptions}
              quickItems={quickItems}
              setQuickItems={setQuickItems}
              templateExclusions={templateExclusions}
              setTemplateExclusions={setTemplateExclusions}
            />
          )}
          {activeScreen === "confirm" && (
            <ConfirmScreen
              event={selectedEvent}
              items={confirmItems}
              index={confirmIndex}
              setIndex={setConfirmIndex}
              completed={completed}
              setCompleted={setCompleted}
              progress={progress}
              voiceEnabled={voiceEnabled}
              setVoiceEnabled={setVoiceEnabled}
              notYetMessage={notYetMessage}
              setNotYetMessage={setNotYetMessage}
              onSpeak={() => speakText(buildSpeechText(confirmItems[confirmIndex]))}
              onDone={() => setEvents((prev) => prev.map((e) => (e.id === selectedEvent?.id ? { ...e, checked: true } : e)))}
            />
          )}
          {activeScreen === "settings" && (
            <SettingsScreen
              prepReminderEnabled={prepReminderEnabled}
              setPrepReminderEnabled={setPrepReminderEnabled}
              prepReminderTime={prepReminderTime}
              setPrepReminderTime={setPrepReminderTime}
              prepDoneToday={prepDoneToday}
              goPrep={()=>setActiveScreen('prep')}
              dailyItems={dailyItems}
              setDailyItems={setDailyItems}
              templates={templates}
              addTemplate={addTemplate}
              updateTemplate={updateTemplate}
              addTemplateItem={addTemplateItem}
              updateTemplateItem={updateTemplateItem}
              removeTemplateItem={removeTemplateItem}
              removeTemplate={removeTemplate}
            />
          )}
        </main>
        <BottomNav activeScreen={activeScreen} setActiveScreen={changeScreen} />
      </div>
    </div>
  );
}

function HomeDashboard({ nextEvent, events, now, templates, onStart }) {
  if (!nextEvent) return <EmptyCard text="今日の出発予定はありません。" />;
  return (
    <section className="space-y-5">
      <h2 className="text-3xl font-black tracking-tight">確認開始</h2>
      <div className={`rounded-[2rem] border-2 p-5 shadow-sm ${getTheme(nextEvent.title).card}`}>
        <div className="flex items-start justify-between gap-3">
          <div>
            <div className="text-sm font-bold text-stone-500">次の出発</div>
            <div className="text-3xl font-black mt-1">{nextEvent.icon} {nextEvent.title}</div>
            <div className="text-4xl font-black mt-2 font-mono">{nextEvent.time}</div>
            <div className="text-lg font-bold text-stone-600 mt-1">{formatUntil(minutesUntil(nextEvent.time, now))}</div>
          </div>
          <StatusBadge checked={nextEvent.checked} />
        </div>
        <button onClick={() => onStart(nextEvent.id)} className="w-full mt-5 rounded-[1.5rem] bg-emerald-700 text-white py-5 text-xl font-black shadow-md">確認する</button>
      </div>
      <div className="space-y-3">
        {events.map((event) => <TimelineEventCard key={event.id} event={event} templates={templates} now={now} onStart={onStart} />)}
      </div>
    </section>
  );
}

function TimelineEventCard({ event, templates, now, onStart }) {
  const template = templates.find((t) => t.id === event.templateId);
  return (
    <button onClick={() => onStart(event.id)} className={`w-full rounded-[1.5rem] p-4 border shadow-sm text-left ${getTheme(event.title).card}`}>
      <div className="flex items-center gap-3">
        <div className={`w-14 h-14 rounded-2xl ${getTheme(event.title).soft} flex items-center justify-center text-2xl`}>{event.icon}</div>
        <div className="flex-1">
          <div><span className="font-mono font-bold mr-2">{event.time}</span><span className="text-2xl font-black">{event.title}</span></div>
          <div className="text-sm text-stone-500 mt-1">{template?.name || "未設定"} ・ {formatUntil(minutesUntil(event.time, now))}</div>
        </div>
        <StatusBadge checked={event.checked} />
      </div>
    </button>
  );
}

function PrepScreen({ setPrepDoneToday,  events, templates, updateEvent, addEvent, duplicateEvent, removeEvent, startConfirmation, eventNameOptions, setEventNameOptions, quickItems, setQuickItems, templateExclusions, setTemplateExclusions }) {
  const [showAdd, setShowAdd] = useState(false);
  return (
    <section className="space-y-4">
      <ScreenTitle title="明日の準備" subtitle="" />
      <div className="rounded-[2rem] bg-white p-5 shadow-sm border border-stone-100">
        <h3 className="text-2xl font-black mb-4">毎日持つもの</h3>
        <div className="grid grid-cols-3 gap-2">
          <div className="rounded-xl bg-stone-100 px-3 py-3 text-center font-bold">鍵</div>
          <div className="rounded-xl bg-stone-100 px-3 py-3 text-center font-bold">スマホ</div>
          <div className="rounded-xl bg-stone-100 px-3 py-3 text-center font-bold">財布</div>
        </div>
      </div>
      
      <button onClick={() => setShowAdd(!showAdd)} className="w-full rounded-2xl bg-emerald-700 text-white py-4 font-black shadow-md">＋出発を追加</button>
      {showAdd && <NewEventForm templates={templates} eventNameOptions={eventNameOptions} setEventNameOptions={setEventNameOptions} addEvent={(data) => { addEvent(data); setShowAdd(false); }} />}
      {events.map((event) => {
        const template = templates.find((t) => t.id === event.templateId);
        const excluded = templateExclusions[event.id] || [];
        const activeCount = (template?.items || []).filter((item) => !excluded.includes(item)).length + (event.specialItems || []).length + 3;
        return (
          <div key={event.id} className={`rounded-[2rem] border shadow-sm p-5 space-y-4 ${getTheme(event.title).card}`}>
            <InlineEventNameEditor event={event} updateEvent={updateEvent} eventNameOptions={eventNameOptions} setEventNameOptions={setEventNameOptions} />
            <UnifiedChooserField label="出発時刻" value={event.time} icon="🕒">
              <input type="time" value={event.time} onChange={(e) => updateEvent(event.id, "time", e.target.value)} className="w-full rounded-xl border px-3 py-3" />
            </UnifiedChooserField>

            <UnifiedChooserField label="シーン別セット" value={`${template?.name || "未設定"}`}>
              <select value={event.templateId} onChange={(e) => updateEvent(event.id, "templateId", e.target.value)} className="w-full rounded-xl border px-4 py-4 mb-3 text-2xl font-black tracking-tight">
                {templates.map((t) => <option key={t.id} value={t.id}>{t.name}</option>)}
              </select>
              <div className="space-y-2">
                {(template?.items || []).map((item) => {
                  const off = excluded.includes(item);
                  return <button key={item} onClick={() => setTemplateExclusions((prev) => ({ ...prev, [event.id]: off ? excluded.filter((x) => x !== item) : [...excluded, item] }))} className="w-full flex justify-between rounded-xl px-3 py-2 bg-white"><span>{off ? "☐" : "☑"} {item}</span><span className="text-xs">{off ? "除外中" : "確認対象"}</span></button>;
                })}
              </div>
            </UnifiedChooserField>
            <TapField label="今日だけ持ち物" value="" valueClassName="text-sm font-bold text-stone-500">
              <SpecialItemsEditor event={event} updateEvent={updateEvent} quickItems={quickItems} setQuickItems={setQuickItems} />
            </TapField>
            
            <div className="rounded-2xl bg-white/70 p-4 font-bold">確認対象 {activeCount}点</div>
            <div className="grid grid-cols-1 gap-2">
              <button onClick={() => startConfirmation(event.id)} className="rounded-2xl bg-emerald-700 text-white py-4 font-black text-lg shadow-md">確認する</button>
              
            </div>
            <button onClick={() => removeEvent(event.id)} className="w-auto px-4 py-2 text-sm rounded-xl bg-white/70 font-bold text-stone-500">この出発準備を削除する</button>
          </div>
        );
      })}
    </section>
  );
}

function NewEventForm({ templates, eventNameOptions, setEventNameOptions, addEvent }) {
  const [selected, setSelected] = useState(eventNameOptions[0]);
  const [custom, setCustom] = useState("");
  const [time, setTime] = useState("09:00");
  const [templateId, setTemplateId] = useState(templates[0]?.id || "");
  const submit = () => {
    const title = custom.trim() || selected.name;
    const icon = custom.trim() ? "🗓️" : selected.icon;
    if (custom.trim() && !eventNameOptions.some((opt) => opt.name === title)) setEventNameOptions((prev) => [...prev.slice(0, 4), { name: title, icon }]);
    addEvent({ title, icon, time, templateId });
  };
  return (
    <div className="rounded-[2rem] bg-white border border-stone-200 p-5 shadow-sm space-y-4">
      <h3 className="text-xl font-black">新しい出発を作る</h3>
      <div className="grid grid-cols-2 gap-2">
        {eventNameOptions.slice(0, 5).map((opt) => <button key={opt.name} onClick={() => { setSelected(opt); setCustom(""); }} className={`rounded-xl px-3 py-3 font-bold text-left ${selected?.name === opt.name && !custom ? "bg-emerald-100" : "bg-stone-100"}`}>{opt.icon} {opt.name}</button>)}
      </div>
      <input value={custom} onChange={(e) => setCustom(e.target.value)} placeholder="＋新規入力" className="w-full rounded-xl border px-3 py-3" />
      <input type="time" value={time} onChange={(e) => setTime(e.target.value)} className="w-full rounded-xl border px-4 py-4 text-2xl font-black tracking-tight" />
      
      <select value={templateId} onChange={(e) => setTemplateId(e.target.value)} className="w-full rounded-xl border px-4 py-4 text-2xl font-black tracking-tight">{templates.map((t) => <option key={t.id} value={t.id}>{t.name}</option>)}</select>
      <button onClick={submit} className="w-full rounded-2xl bg-emerald-700 text-white py-4 font-black shadow-md">この内容で追加</button>
    </div>
  );
}

function InlineEventNameEditor({ event, updateEvent, eventNameOptions, setEventNameOptions }) {
  const [open, setOpen] = useState(false);
  const [custom, setCustom] = useState("");
  const choose = (opt) => { updateEvent(event.id, "title", opt.name); updateEvent(event.id, "icon", opt.icon); setOpen(false); };
  const addCustom = () => {
    const name = custom.trim();
    if (!name) return;
    const opt = { name, icon: "🗓️" };
    setEventNameOptions((prev) => [...prev.slice(0, 4), opt]);
    choose(opt);
    setCustom("");
  };
  return (
    <div>
      <div className="text-xs font-bold text-stone-500 mb-1">出発名</div>
      <button onClick={() => setOpen(!open)} className="w-full rounded-xl bg-white/70 border px-4 py-3 flex justify-between items-center font-black text-3xl tracking-tight"><span>{event.icon} {event.title}</span><span className="text-sm font-bold px-3 py-1 rounded-full bg-stone-100 border text-stone-600">変更</span></button>
      {open && <div className="mt-3 rounded-2xl bg-white border p-3 space-y-2 shadow-sm">
        {eventNameOptions.slice(0, 5).map((opt, index) => <div key={opt.name} className="flex gap-2"><button onClick={() => choose(opt)} className="flex-1 text-left rounded-xl px-4 py-3 bg-stone-100 font-bold">{opt.icon} {opt.name}</button><button onClick={() => index > 0 && setEventNameOptions((prev) => { const arr = [...prev]; [arr[index - 1], arr[index]] = [arr[index], arr[index - 1]]; return arr; })} className="px-3 rounded-xl bg-stone-200">↑</button><button onClick={() => setEventNameOptions((prev) => prev.filter((x) => x.name !== opt.name))} className="px-3 rounded-xl bg-stone-200">×</button></div>)}
        <input value={custom} onChange={(e) => setCustom(e.target.value)} placeholder="＋新規入力" className="w-full rounded-xl border px-3 py-3" />
        <button onClick={addCustom} className="w-full rounded-xl bg-emerald-700 text-white py-3 font-black">追加</button>
      </div>}
    </div>
  );
}





function SpecialItemsEditor({ event, updateEvent, quickItems, setQuickItems }) {
  const addItem = (item) => {
    if (!item) return;
    if (!(event.specialItems || []).includes(item)) updateEvent(event.id, "specialItems", [...(event.specialItems || []), item]);
    if (!quickItems.includes(item)) setQuickItems((prev) => [item, ...prev].slice(0, 10));
  };
  return <div className="space-y-3">{(event.specialItems || []).map((item, index) => <div key={index} className="flex gap-2"><input value={item} onChange={(e) => { const arr = [...event.specialItems]; arr[index] = e.target.value; updateEvent(event.id, "specialItems", arr); }} className="flex-1 rounded-xl border px-3 py-2" /><button onClick={() => updateEvent(event.id, "specialItems", event.specialItems.filter((_, i) => i !== index))} className="px-3 rounded-xl bg-stone-100">削除</button></div>)}<button onClick={() => addItem("新しい持ち物")} className="w-full rounded-xl bg-amber-300 py-3 font-black">＋追加</button><div className="text-xs font-bold text-stone-500">候補</div><div className="flex flex-wrap gap-2">{quickItems.map((item,index)=><div key={item} className="flex items-center gap-1"><button onClick={()=>addItem(item)} className="rounded-full bg-stone-200 px-3 py-2 text-sm font-bold">{item}</button><button onClick={()=>setQuickItems(prev=>prev.filter((_,i)=>i!==index))} className="text-xs px-2 py-1 rounded-full bg-white border">×</button></div>)}</div></div>;
}

function ConfirmScreen({ event, items, index, setIndex, completed, setCompleted, progress, voiceEnabled, setVoiceEnabled, notYetMessage, setNotYetMessage, onSpeak, onDone }) {
  if (!event) return <EmptyCard text="確認する出発がありません。" />;
  if (!items.length) return <EmptyCard text="確認する持ち物がありません。" />;
  const current = items[index];
  const finish = () => { setCompleted(true); onDone(); };
  if (completed) return <section className="space-y-5"><div className={`rounded-[2rem] p-8 shadow-sm border text-center ${getTheme(event.title).card}`}><div className="text-5xl mb-4">✅</div><div className="inline-block rounded-full bg-white/70 px-4 py-2 text-sm font-black mb-4">{event.title} チェック済み</div><h2 className="text-3xl font-black mb-3">出発確認完了！</h2><p className="text-stone-500">落ち着いて出発できます。</p></div><ProgressBar value={100} label={`${items.length} / ${items.length}項目 完了`} /></section>;
  return <section className="space-y-5"><div className="flex justify-between gap-3"><ScreenTitle title={`${event.icon} ${event.title}の確認`} subtitle="1つずつ確認します。" /><VoiceToggle enabled={voiceEnabled} setEnabled={setVoiceEnabled} /></div><ProgressBar value={progress} label={`${index + 1} / ${items.length}確認中`} /><div className={`rounded-[2rem] p-6 shadow-sm border text-center space-y-5 ${getTheme(event.title).card}`}><button onClick={onSpeak} className="mx-auto w-20 h-20 rounded-full bg-white border shadow-sm text-4xl">🔊</button><p className="text-sm font-bold text-stone-400">タップで再読み上げ</p><h2 className="text-3xl font-black leading-snug">{current.name}、<br />持った？</h2><p className="inline-block rounded-full bg-white/80 px-4 py-2 text-sm font-bold text-stone-500">{current.category}</p></div>{notYetMessage && <div className="rounded-[1.5rem] bg-white p-4 shadow-sm"><p className="font-bold">大丈夫です。</p><p className="text-stone-500">取りに行ってから、もう一度確認しましょう。</p></div>}<button onClick={() => index + 1 >= items.length ? finish() : setIndex(index + 1)} className="w-full rounded-[1.5rem] bg-emerald-700 text-white py-5 text-xl font-black shadow-md">持った</button><button onClick={() => setNotYetMessage(true)} className="w-full rounded-[1.5rem] bg-white py-5 text-xl font-black text-stone-600">まだ</button></section>;
}

function SettingsScreen({ prepReminderEnabled, setPrepReminderEnabled, prepReminderTime, setPrepReminderTime, prepDoneToday, goPrep, dailyItems, setDailyItems, templates, addTemplate, updateTemplate, addTemplateItem, updateTemplateItem, removeTemplateItem, removeTemplate }) {
  return (
    <section className="space-y-5">
      <div className="rounded-[2rem] bg-white p-5 shadow-sm border border-stone-100 space-y-4">
        <h2 className="text-xl font-black">夜の準備リマインド</h2>
        <div className="flex justify-between items-center">
          <span className="font-bold">通知</span>
          <button
            onClick={() => setPrepReminderEnabled(!prepReminderEnabled)}
            className={`rounded-full px-4 py-2 font-bold ${prepReminderEnabled ? "bg-emerald-100" : "bg-stone-200"}`}
          >
            {prepReminderEnabled ? "ON" : "OFF"}
          </button>
        </div>
        <input
          type="time"
          value={prepReminderTime}
          onChange={(e) => setPrepReminderTime(e.target.value)}
          className="w-full rounded-xl border px-3 py-3"
        />
        <div className="rounded-2xl bg-[#f7f3ec] p-4 text-sm">
          <div className="font-bold mb-1">通知文</div>
          「明日の準備はできましたか？」
        </div>
        {prepDoneToday && (
          <div className="rounded-xl bg-emerald-50 p-3 font-bold text-emerald-700">
            今日は準備完了のため通知停止
          </div>
        )}
        <button onClick={goPrep} className="w-full rounded-xl bg-stone-200 py-3 font-bold">
          通知タップを試す（明日の準備へ）
        </button>
      </div>

      <ScreenTitle title="設定" subtitle="毎日持ち物とシーン別セットを管理します。" />
      <EditableList title="毎日持つもの" items={dailyItems} setItems={setDailyItems} />
      <TemplateEditor
        templates={templates}
        addTemplate={addTemplate}
        updateTemplate={updateTemplate}
        addTemplateItem={addTemplateItem}
        updateTemplateItem={updateTemplateItem}
        removeTemplateItem={removeTemplateItem}
        removeTemplate={removeTemplate}
      />
    </section>
  );
}

function EditableList({ title, items, setItems }) {
  return <div className="rounded-[2rem] bg-white p-5 shadow-sm border border-stone-100 space-y-3"><div className="flex justify-between"><h2 className="font-bold text-lg">{title}</h2><button onClick={() => setItems((prev) => [...prev, "新しい持ち物"])} className="rounded-full bg-stone-200 px-3 py-2 text-sm font-bold">追加</button></div>{items.map((item, index) => <div key={index} className="flex gap-2"><input value={item} onChange={(e) => setItems((prev) => prev.map((x, i) => i === index ? e.target.value : x))} className="flex-1 rounded-2xl border px-4 py-3" /><button onClick={() => setItems((prev) => prev.filter((_, i) => i !== index))} className="rounded-2xl bg-stone-100 px-3">削除</button></div>)}</div>;
}

function TemplateEditor({ templates, addTemplate, updateTemplate, addTemplateItem, updateTemplateItem, removeTemplateItem, removeTemplate }) {
  return <div className="rounded-[2rem] bg-white p-5 shadow-sm border border-stone-100 space-y-4"><div className="flex justify-between"><h2 className="text-xl font-black">シーン別セット</h2><button onClick={addTemplate} className="rounded-full bg-stone-200 px-3 py-2 font-bold">追加</button></div>{templates.map((template) => <div key={template.id} className="rounded-2xl bg-[#f7f3ec] p-4 space-y-3"><div className="flex gap-2"><input value={template.name} onChange={(e) => updateTemplate(template.id, "name", e.target.value)} className="flex-1 rounded-xl px-3 py-2 border font-bold" /><button onClick={() => removeTemplate(template.id)} className="px-3 rounded-xl bg-white">削除</button></div>{template.items.map((item, index) => <div key={index} className="flex gap-2"><input value={item} onChange={(e) => updateTemplateItem(template.id, index, e.target.value)} className="flex-1 rounded-xl px-3 py-2 border" /><button onClick={() => removeTemplateItem(template.id, index)} className="px-3 rounded-xl bg-white">削除</button></div>)}<button onClick={() => addTemplateItem(template.id)} className="w-full rounded-xl bg-stone-200 py-2 font-bold">持ち物を追加</button></div>)}</div>;
}

function UnifiedChooserField({ label, value, icon, children }) {
  const [open,setOpen]=useState(false);
  return (
    <div className="rounded-2xl bg-white/70 p-4">
      <div className="text-xs font-bold text-stone-500 mb-1">{label}</div>
      <button onClick={()=>setOpen(!open)} className="w-full rounded-xl bg-white border px-4 py-3 flex justify-between items-center text-3xl font-black tracking-tight">
        <span>{icon} {value}</span>
        <span className="text-sm font-bold px-3 py-1 rounded-full bg-stone-100 border text-stone-600">変更</span>
      </button>
      {open && <div className="mt-3">{children}</div>}
    </div>
  );
}

function TapField({ label, value, children, valueClassName }) {
  return (
    <div className="rounded-2xl bg-white/70 p-4">
      <div className="text-2xl font-black tracking-tight">{label}</div>
      <div className={`${valueClassName || 'text-3xl font-black tracking-tight'} mt-2 mb-4`}>
        {value}
      </div>
      {children}
    </div>
  );
}
function StatusBadge({ checked }) {
  return (
    <span className={`shrink-0 rounded-full px-4 py-2 text-xs font-black ${checked ? "bg-emerald-200 text-emerald-800 border border-emerald-300" : "bg-amber-100 text-amber-800 border border-amber-300"}`}>
      {checked ? "✓ 確認完了" : "○ 確認待ち"}
    </span>
  );
}
function ProgressBar({ value, label }) { return <div className="rounded-[2rem] bg-white p-4 shadow-sm border"><div className="flex justify-between text-sm font-bold text-stone-500 mb-2"><span>進捗</span><span>{label}</span></div><div className="h-4 rounded-full bg-stone-100 overflow-hidden"><div className="h-full rounded-full bg-emerald-700" style={{ width: `${value}%` }} /></div></div>; }
function VoiceToggle({ enabled, setEnabled }) { return <button onClick={() => setEnabled(!enabled)} className={`shrink-0 rounded-full px-4 py-2 font-bold ${enabled ? "bg-emerald-100" : "bg-stone-200"}`}>音声 {enabled ? "ON" : "OFF"}</button>; }
function ScreenTitle({ title, subtitle }) { return <div><h2 className="text-3xl font-black tracking-tight mb-2">{title}</h2><p className="text-stone-500 leading-relaxed">{subtitle}</p></div>; }
function EmptyCard({ text }) { return <div className="rounded-[2rem] bg-white p-6 shadow-sm border text-center text-stone-500 font-bold">{text}</div>; }
function BottomNav({ activeScreen, setActiveScreen }) {
  const nav = [{ key: "prep", label: "明日の準備", icon: "📋" }, { key: "check", label: "確認開始", icon: "✅", fab: true }, { key: "settings", label: "設定", icon: "⚙️" }];
  return <nav className="fixed bottom-0 left-1/2 -translate-x-1/2 w-full max-w-md bg-white/95 border-t px-4 py-3"><div className="grid grid-cols-3 items-end gap-2">{nav.map((item) => item.fab ? <button key={item.key} onClick={() => setActiveScreen(item.key)} className="-mt-8 flex flex-col items-center"><div className={`w-20 h-20 rounded-full flex items-center justify-center text-3xl shadow-lg ${activeScreen === item.key ? "bg-emerald-700" : "bg-stone-700"} text-white`}>{item.icon}</div><div className="mt-1 text-xs font-black">確認開始</div></button> : <button key={item.key} onClick={() => setActiveScreen(item.key)} className={`rounded-2xl py-3 flex flex-col items-center gap-1 text-xs font-bold ${activeScreen === item.key ? "bg-stone-200" : "text-stone-400"}`}><div className="text-xl">{item.icon}</div>{item.label}</button>)}</div></nav>;
}
