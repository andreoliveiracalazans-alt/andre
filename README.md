import { createClient } from 'https://esm.sh/@supabase/supabase-js@2';
import { SUPABASE_URL, SUPABASE_KEY } from './supabase-config.js';

const supabase = createClient(SUPABASE_URL, SUPABASE_KEY);
const el = document.getElementById('blog-preview');

function escapeHtml(str) {
  const div = document.createElement('div');
  div.textContent = str || '';
  return div.innerHTML;
}

async function loadPreview() {
  const { data, error } = await supabase
    .from('blog_posts')
    .select('slug, title, excerpt, category, published_at')
    .eq('published', true)
    .order('published_at', { ascending: false })
    .limit(3);

  if (error || !data || data.length === 0) {
    el.innerHTML = '<div class="post-empty">Em breve, novos artigos sobre Direito do Trabalho e Direito de Família.</div>';
    return;
  }

  el.innerHTML = data.map(post => `
    <a class="post-card" href="blog/post/?slug=${encodeURIComponent(post.slug)}">
      <div class="post-card-body">
        <span class="post-cat">${escapeHtml(post.category)}</span>
        <h3>${escapeHtml(post.title)}</h3>
        <p class="post-excerpt">${escapeHtml(post.excerpt || '')}</p>
        <span class="post-read">Ler artigo →</span>
      </div>
    </a>
  `).join('');
}

loadPreview();
