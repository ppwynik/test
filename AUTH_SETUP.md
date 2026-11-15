# Konfiguracja logowania e-mail w aplikacji Praca

Aplikacja korzysta z Supabase Auth: rejestracja przez e-mail i hasło, potwierdzenie adresu e-mail oraz reset hasła.

## Konfiguracja Supabase

1. Otwórz Authentication → URL Configuration.
2. Ustaw **Site URL** na publiczny adres strony aplikacji (adres, pod którym otwierasz plik index.html).
3. W **Redirect URLs** dodaj ten sam adres oraz wariant obejmujący ścieżki aplikacji. Dla GitHub Pages będzie to np. `https://NAZWA-UZYTKOWNIKA.github.io/NAZWA-REPOZYTORIUM/**`.
4. W Authentication → Sign In / Providers → Email pozostaw włączone Email provider i włączone **Confirm email**.
5. W Authentication → Email Templates sprawdź, czy szablon Confirm signup używa linku `{{ .ConfirmationURL }}`.
6. Wysyłka wiadomości wymaga działającego SMTP. Domyślny serwer testowy Supabase ma limity; do regularnego użycia skonfiguruj własny SMTP.

## Co obsługuje aplikacja

- Rejestrację e-mail + hasło; po rejestracji pokazuje komunikat o konieczności kliknięcia linku z poczty.
- Logowanie zweryfikowanym adresem e-mail i hasłem.
- Reset hasła przez wiadomość e-mail i formularz ustawienia nowego hasła na tej samej stronie.
- Osobna podstrona callback nie jest potrzebna — link potwierdzający i resetujący wraca na aktualny adres index.html.

Adres przekierowania jest pobierany automatycznie z aktualnego adresu strony (`window.location.origin + window.location.pathname`). Musi więc znajdować się na liście Redirect URLs w Supabase.